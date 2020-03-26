---
title: 阿里云hexo
date: 2019-09-06 14:57:32
author: 玄机
tags: 
- 服务器
- ecs
- 阿里云
categories: 服务器
---

> 今天备案通过，故重新整顿了下博客，记录下上午的成果\_

<!-- more -->

# 备案脚标的添加

1. 以前添加需要自己复制代码，现在简单多了，hexo 的 next 主题直接可以添加备案信息且还可以下载图标，直接放图
   ![](https://yimg.xjdd.xyz//备案图.png)
   成果就是这样子：
   ![](https://yimg.xjdd.xyz//20190906150639.png)

# 搞图床

第二件事就是 **搞图床**,
如今备案了就直接使用国内的 cdn 就好了。
我使用的是[七牛云](https://www.qiniu.com)和[又拍云](https://www.upyun.com)
过程也不复杂，就是注册就完事了
比较复杂的就是配置 CNAME

1. 七牛云为例子，记录一下
   ![](https://yimg.xjdd.xyz//20190906151344.png)
   注册对象存储，会给你个测试域名，以前不懂，以前的图片都挂了，因为只有三十天的使用时期，所以还是要绑定域名，才能避免这一切。
   因为并不使用七牛云的 cdn 服务，所以直接创个二级域名就好。
   ![](https://yimg.xjdd.xyz//20190906151657.png)
2. 现在创建成功，接下来就是域名服务商的操作了。
   ![](https://yimg.xjdd.xyz//20190906151833.png)
   现在就是添加解析的时候了，我使用的是阿里云的域名所以打开阿里云的控制台 中的*域名*管理进行操作
   ![](https://yimg.xjdd.xyz//20190906152032.png)
   点**解析**，**添加记录**
   ![](https://yimg.xjdd.xyz//20190906152157.png)
   如图所示，主机记录填写**二级域名**，记录值填写七牛云的所注册的域名的**CNAME**值。
   添加后返回七牛云，刷新界面。就 OK 了。
   现在无非就是找款软件上传图了
   我使用的是

**[picgo](https://github.com/Molunerfinn/PicGo/releases)**

点击就可以下载了。设置什么的文档介绍的很详细，就不细说了。

# https 的小锁添加

作为一个轻微强迫症，看到 F12 里的黄字警告和浏览器栏的警告这怎么可以忍！！！
hexo 本身不支持添加 https，
所以还是得自己搞：

1. 阿里云，七牛云，又拍云都有免费的 ssl 证书申请，咱搞免费就 OK 了。
   ![](https://yimg.xjdd.xyz//20190906153318.png) 阿里云的
2. 然后返回证书界面，点申请
   ![](https://yimg.xjdd.xyz//20190906153536.png)
   填信息，过验证 就 OK 了
   ![](https://yimg.xjdd.xyz//20190906153711.png)
3. 申请下来后下载证书
   ![](https://yimg.xjdd.xyz//20190906153817.png)
   浏览器的端的操作就结束了
4. 现在到了服务器端的操作，修改 Nginx 的配置问题
   个人对 Linux 系统操作不太熟悉，所以使用了 xshell 系列的 xftp 进行操作。。。
   先是连接服务器呗 然后打开 xftp 一般来说 nginx 都在`/etc/nginx`目录下
   ![](https://yimg.xjdd.xyz//20190906154242.png)
   现在打开`nginx.conf`进行编辑了（记事本，vscode 都可以，一个直接改，一个下载到本地然后传回去）。
   ![](https://yimg.xjdd.xyz//20190906154822.png)
   现在打开自己的网站，http 加上 s 就可以使用了
   还可以

```
 server {
    listen       80;
    server_name  xjdd.xyz;
    return 301 https://xjdd.xyz$request_uri; //在这里添加语句，http自动跳转https

    root         /var/www/hexo;

    # Load configuration files for the default server block.


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

接下来就是解决图床上传的问题了，七牛云的上传图片不带 s，所以。。
我注册又拍云的账号，又拍云免费的话需要打广告，页脚添加链接，会点 html 就行了。
需要注册

**[又拍云联盟](https://www.upyun.com/league)**

操作和七牛云差不多，就是要开启 https，加上注册一个免费证书。现在我还在等那个又拍云联盟的通过。先写到这里
