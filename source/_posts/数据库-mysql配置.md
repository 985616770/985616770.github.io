---
title: Apache2.4.34 + php 7.28 + MySQL8.0.12 安装及配置
date: 2018-08-31 13:39:59
tags: 
- 服务端
- php
- Apache
- MySQL
categories: 数据库
---

## Apache2.4.34 的安装及配置

### 1.基本安装

最新的 Apache 已经不提供 Windows 的安装版本,所以我们这里使用的是解压版

> -下载地址：https://www.apachelounge.com/download/ -使用说明：https://httpd.apache.org/docs/current/platform/windows.html

安装方式如下

<!-- more -->

```html
1.注意：需要使用管理员身份运行命令行！！！
2. 切换到 Apache 解压路径中的 bin 目录 3.# $ cd <解压目录>/bin
4.安装 Apache 服务，‐n 参数是指定服务名称 5.# $ httpd.exe ‐k install ‐n "Apache"
6.如果需要卸载 Apache，可以执行以下命令 7.# $ httpd.exe ‐k uninstall ‐n "Apache"
```

执行安装命令过后会报一个错，原因是默认的配置文件有问题，需要先调整一下配置文件 ==conf/httpd.conf== ，才能正常启动服务。

找到 Apache 解压目录中的 conf 目录下的 httpd.conf 文件，定位到 37 行，将 c:/Apache24 改为解压目录，我这里解压到路径是 C:/Develop/apache ，所以我这里修改

修改完以后，执行以下命令重新测试配置文件是否通过。

> \$ httpd.exe ‐t

这里依然报错：

随即，我们发现这个配置文件中有很多默认配置选项中的路径都是 c:/Apache24 ，所以我们批量都修改为我们解
压的目录路径。
然后重新执行 httpd.exe -t 测试配置文件，这时候应该提示 Syntax OK 。

> 如果有关于 `ServerName` 的警告提示，不用管它，暂时还不会影响我们接下来的使用和操作。

接着运行以下命令重新启动 Apache 服务：

```txt
# 注意：需要使用管理员身份运行命令行！！！
$ httpd.exe ‐k start ‐n "Apache"
# 重新启动 Apache 服务
$ httpd.exe ‐k restart ‐n "Apache"
# 停止 Apache 服务
$ httpd.exe ‐k stop ‐n "Apache"
```

回到浏览器中，地址栏输入：http://localhost/，回车访问，这时正常应该看到 It works!

如果无法访问 请查看 80 端口是否被占用

> 可以直接在 httpd.conf 中改端口 访问

注意:

```
1.确保配置文件语法检查通过
2.确保  80 端口没有被其他程序占用
3.确保防火墙允许  80 端口的请求，或者干脆关掉防火墙
4.如果出现 Forbidden 情况，确保配置文件  httpd.conf 中 247 行（ DocumentRoot 之后）的  Directory 配置的与  DocumentRoot 路径相同
5.我们在开发阶段大多数都是自己访问自己机器上的网站，那这种情况下，我们既是服务端又是客户端。 对于新手来说，最常见的问题就是分不清楚哪是客户端应该有的，哪是服务端应该有的。这种时候一定要保持清醒，客户端局限在浏览器窗口，代码以及 Apache 相关的文件和配置都是放在服务端的。
```

#### 网站根目录

> 网站根目录就是存放我们网站文件的最顶层目录，通常 URL 中域名后面的第一个斜线对应（映射）的就是网站根目录。
> 默认文档指的是我们在访问某一个目录时（没有指定具体的文件），默认访问的文件叫做默认文档
> 注：动态网站情况会比较特殊，需要单独考虑，不一定是这个规则。

默认 Apache 的网站根目录是安装目录中的 htdocs 文件夹，为了方便对网站文件的管理，一般我们会将其设置在一个自定义目录中（如果你不介意其实不修改也无所谓）。
如果需要设置网站根目录，可以通过修改配置文件 httpd.conf 中的网站根目录选项切换。

#### 默认文档

> 当客户端访问的是一个目录而不是具体文件时，服务端默认返回这个目录下的某个文档（文件），这个文档就称之为 默认文档。

配置文件 httpd.conf 的 280 行的 DirectoryIndex ，默认文档可以配置多个（有前到后依次去找，找到为止，如果没找到任何一个则启用目录浏览）：

### 2.虚拟主机的配置

如果一台机器上只有一个网站的话，没有任何问题，但是如果想要在一台机器上部署多个站点，就必须通过配置虚拟主机的方式解决。

> 由于后期对虚拟主机的配置操作非常常见，所以我们一般将虚拟主机的配置单独放到一个配置文件中，然后在主配置文件中引入，避免破坏主配置文件中的其他配置。
> Include conf/extra/httpd-vhosts.conf 配置的作用就将另外一个配置文件引入（使其生效）

具体的操作方式就是在主配置文件 httpd.conf 的 505 行取消注释：

然后找到 Apache 的虚拟主机配置文件，添加一个如下的虚拟主机配置节点，然后重新启动 Apache。

> 这个文件中有两个默认的示例配置，可以注释掉

如果真的要使用 baixiu.com 这个域名的话，就只能通过修改 hosts 文件达到目的，原因很简单：这个域名不是我们自己的，我们没有办法修改这个域名在公网上的 DNS。

具体操作

1.改成所需的都域名和端口

添加内容

```
<Directory "F:/study/zixue/php">
     Options Indexes FollowSymLinks
     AllowOverride None
     Require all granted
 </Directory>
```

2.更改系统文件 hosts

末尾添加

```
#配置
127.0.0.1 xuanji.io
```

如果虚拟主机的端口使用的不是 80 ，则需要在主配置文件中添加一个对这个端口的监听：

## PHP7.28 的安装及配置

##### 1.基本安装

官网下载 PHP 的版本

> https://windows.php.net/download#php-7.2

最好解压在与服务器同一个文件夹中 方便管理(_纯英文路径_)

接下来,在 Apache 中添加支持

```
httpd.conf中
# php support
LoadModule php7_module C:/Develop/php/php7apache2_4.dll
#最好手打 容易出错
```

然后在 `<IfModule mime_module>` 节点中添加 `.php` 扩展名解析支持

```
# parse .php files
AddType application/x‐httpd‐php .php
```

默认文档配置节点 `<IfModule dir_module>` 中添加 `index.php`

> 默认文档指的是在访问一个目录而不是具体文件名时，默认执行的文件名

```
<IfModule dir_module>
    DirectoryIndex index.html index.php
</IfModule>
```

重启 Apache,打开浏览器测试

## MySQL8.0 的安装

##### 1.基本安装

1.解压到纯英文路径(最好还是一个目录下)

> 下载地址：https://dev.mysql.com/downloads/mysql/

2.解压目录添加 my.ini

参考：

> http://www.cnblogs.com/Ray-xujianguo/p/3322455.html >https://gist.github.com/hanjong/1205199 >https://dev.mysql.com/doc/refman/5.5/en/mysqld-option-tables.html

```
[mysqld]
# MySQL 安装目录
basedir=C:/Develop/mysql
# 数据文件所在目录
datadir=C:/Develop/mysql/data
```

3.以管理员身份运行 CMD 执行以下命令，安装一个 MySQL 服务

```
# 定位到安装目录下的 bin 文件夹
$ cd <MySQL安装目录>/bin
# 初始化数据所需文件以及获取一个临时的访问密码
$ mysqld ‐‐initialize ‐‐user=mysql ‐‐console
# 将 MySQL 安装为服务 可以指定服务名称
$ mysqld ‐‐install MySQL
启动服务
$ net start mysql
```

4.登入 MySQL 服务器，重置密码

```
# 先通过用户名密码进入 MySQL 操作环境
$ mysql ‐u root ‐p
Enter password: # 输入临时密码
# 设置数据库访问密码，一定要加分号
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
```

注意:

删除 全局删除 mysql 服务

> sc delete 服务名称

##### 2.与 php 连接起来

1.如果需要使用 MySQLi 扩展，需要在 php.ini 文件中打开这个扩展（解除注释）

如果没有 php.ini 将下方的两个后缀改成 ini 即可

在 php.ini 中查找

解开注释即可

还有在这注意 Apache 是否已经把载入的设置在 php 目录下，如果无效在 apache 末尾添加

> PHPIniDir “php.ini 的路径”php.ini

还有如果无效，请查看 php.ini 中的拓展路径是否打开（添加绝对路径 C:\fuwuqi\php7.2）

然后在服务器中打开 php 文件

显示这个就成功开启了连接

出现无法连接数据库的解决方法

输入命令

```shell
ALTER USER `root`@`localhost` IDENTIFIED WITH caching_sha2_password BY '123456';
grant all privileges on *.* to ‘root’@’localhost’;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
GRANT ALL ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
SHOW GRANTS FOR 'root'@'localhost';
flush privileges;
create user 'zp'@'%' identified by '123456';
update user set host = "localhost" where user = "root";
select host, user, authentication_string, plugin from user;
Delete FROM user Where User='zp' and Host='%';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY '123456' WITH GRANT OPTION;
```
