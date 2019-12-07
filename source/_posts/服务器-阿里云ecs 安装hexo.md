---
title: 阿里云ECS安装HEXO
date: 2018-10-30 17:39:48
tags:
  - 服务器
  - ecs
  - 阿里云
categories: 服务器
---
<!-- more -->
## 安装 Git(服务端)

```
$ yum install git
```

8、查看 git 版本

```
$ git --version
```

<!-- more -->

## 安装 hexo(window)

先切换镜像

```
# npm config set registry http://registry.npm.taobao.org/
更换
# npm get registry
查看地址
```

安装完上面两项后，只需要使用 npm 即可完成 Hexo 的安装:

```
$ npm install -g hexo-cli #全局安装hexo
```

安装完成后，新建博客文件夹并初始化 hexo 文件夹：

```
$ mkdir <floder>
$ hexo init <folder>
$ cd <folder>
$ npm install
```

hexo 的操作比较简单 自行看文档

## git 创建(服务端)

### 创建 git 用户

**1.创建一个 git 用户，并根据提示设置密码，用来专门运行 git 服务:**

```
$ adduser git
```

**2.赋予 git 用户 sudo 权限**

```
$ chmod 740 /etc/sudoers
$ vim /etc/sudoers #编辑文档
```

找到以下内容：

```
## Allow root to run any commands anywhere
root    ALL=(ALL)     ALL
```

在下面添加一行：
`git ALL=(ALL) ALL`

保存退出后改回权限：

```
$ chmod 400 /etc/sudoers
```

**3.切换用户，配置 SSH**

使用 `su git` 切换到 git 用户，再执行下列操作：

```
# 切换到git用户目录
$ cd /home/git
# 创建.ssh文件夹
$ mkdir ~/.ssh
# 创建authorized_keys文件并编辑
$ vim ~/.ssh/authorized_keys
# 如果你还没有生成公钥，那么首先在本地电脑中执行 cat ~/.ssh/id_rsa.pub | pbcopy生成公钥
# 再将公钥复制粘贴到authorized_keys
# 保存关闭authorized_keys后，修改相应权限
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys
```

然后可以通过本地 Git Bash 执行 ssh 命令测试是否可以免密登录

```
$ ssh -v git@服务器ip地址:端口
```

这样 git 用户就添加好了。

### 建立 git 裸库

```
# 回到git目录
$ cd /home/git
# 使用git用户创建git裸仓库，以blog.git为例
$ git init --bare blog.git
```

### 检查用户组权限

我们的 git 裸仓库已经建立好了，离成功又近了一步。为了以防万一，我们要检查一下之前的 blog.git、.ssh、blog 目录的用户组权限是否都为 git:git

```
# 还记得/var/www/吗？这是之前配置nginx时，我们自己选定的网站根目录，请依据你自己的设置更改
ll -a /var/www/
ll -a /home/git/
```

如果有哪个不是，执行下面相应的命令后再查看

```
sudo chown git:git -R /var/www/blog
sudo chown git:git -R /home/git/blog.git
```

### 使用 git-hooks 同步网站根目录

简单来说，我们使用一个钩子文件：`post-receive`，每当 git 仓库接收到内容的时候，就会自动调用这个钩子，把内容同步到网站根目录。

在 git 用户下执行：

```
# 新建一个post-receive文件并编辑
$ vim ~/blog.git/hooks/post-receive
```

在里面输入以下内容，注意修改为自己的设置：

```
#!/bin/sh
git --work-tree=/data/www/blog --git-dir=/home/git/blog.git checkout -f
```

保存退出后，执行：

```
$ chmod +x post-receive

```

赋予这个文件可执行权限。

好了，以上就是服务器端需要配置的内容。我们还差最后一步就可以完成整个部署了！

## 安装 ngnix

域名和服务器准备好之后，就是安装网站容器了，我选择的是 nginx。nginx 的安装过程非常简单，nginx 的安装有两种方式，一种是采用源代码安装，一种是采用安装包。我图省事采用了安装包安装，nginx 安装步骤如下：

```
$ yum -y install nginx
```

在执行了以上的命令之后，就安装成功了，有木有很简单，安装成功后，输入启动命令：

```
$ systemctl start nginx.service #启动
```

访问你的机器 ip，如果看到如下页面，就说明已经安装成功了。

编辑 ngnix 服务器配置文件

```
$ vi /etc/nginx/nginx.conf
```

```
server {
    listen       80 default_server;
    listen       [::]:80 default_server;
    # 网站域名 配置自己的域名即可
    server_name  xjdd.xyz www.xjdd.xyz;
    # 网站目录 自定义目录即可
    root         /var/www/blog;
    index        index.html index.htm index.txt;

    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }
}
```

```
ngnix命令
service nginx restart #重启服务器
systemctl start nginx.service #启动服务器
nginx -t #测试
$ sudo nginx -t  #查看nginx配置路径，宝塔面板安装nginx非下列路径
$ sudo vim /etc/nginx/nginx.conf

```

## 配置本地 Hexo 的\_config.yml

非常简单，只需要找到本地 Hexo 博客的站点配置文件\_config.yml，找到以下内容并修改：

```
deploy:
  type: git
  repo: git@你的服务器IP:/home/git/blog.git
  branch: master
```

保存后，剩下的就是 Hexo 的日常操作了，这里就不赘述了，写完文章后，在你的本地博客根目录执行以下命令：

```

hexo clean
hexo g -d

```

就可以实现线上博客的自动更新了！一切搞定！

## 一些注意点和小坑

很多时候我们没这么幸运，博客搭建过程中总会出现无数的坑。

### CentOS 和 Ubuntu

如果你的 VPS 系统是 Ubuntu，那么`yum`命令肯定要换成`apt-get`。

> 一般来说著名的 linux 系统基本上分两大类：
> 1.RedHat 系列：Redhat、Centos、Fedora 等
> 2.Debian 系列：Debian、Ubuntu 等
> RedHat 系列
> 1 常见的安装包格式 rpm 包,安装 rpm 包的命令是“rpm -参数”
> 2 包管理工具 yum
> 3 支持 tar 包
> Debian 系列
> 1 常见的安装包格式 deb 包,安装 deb 包的命令是“dpkg -参数”
> 2 包管理工具 apt-get
> 3 支持 tar 包

### vim: command not found

系统自带的 vim 未正确安装

输入`rpm -qa|grep vim`命令, 如果 vim 已经正确安裝,会返回下面的三行代码:

```
root@server1 [~]# rpm -qa|grep vim
vim-enhanced-7.0.109-7.el5
vim-minimal-7.0.109-7.el5
vim-common-7.0.109-7.el5
```

如果少了其中的某一条,比如`vim-enhanced`,就用命令`yum -y install vim-enhanced`来安裝缺少的那一个。

如果上面的三条一条都沒有返回, 那就直接用`yum -y install vim*`命令吧！

### Permission denied

如果 git 用户出现类似权限不够被拒绝访问的问题，直接试试使用 sudo 权限吧！

例如：在创建文件夹的时候出现权限不够的问题，最简单的解决方法就是`sudo mkdir 文件夹名`

但还是具体问题具体分析，多多谷歌。

### 一切正常，但 deploy 后网页无法显示

首先要查看一下服务器网站根目录下是否有 Hexo 的静态文件。

如果没有，说明 git 配置出现问题，再仔细查找配置上的原因。

如果已经传入了静态文件，说明可能是服务器 nginx 等环境配置出现问题，这种情况排查起来比较困难，一个简单粗暴的办法就是试试一键安装 LNMP(安装方法请自行百度+谷歌)。

> LNMP 代表的就是：Linux 系统下 Nginx+MySQL+PHP 这种网站服务器架构
> 同样还有 LAMP，它代表的是 Linux+Apache+Mysql/MariaDB+Perl/PHP/Python
