---
title: ECS自建图床
tags:
- ecs
- 阿里云
- 图床
date: 2018-12-01 07:59:35
categories: 服务器
---


## 自建图床 chevereto

<!-- more -->

如果你有多余的 VPS，或者带宽足够，可以考虑拿来搭个图床。我个人就是使用的 Vultr 的 5 刀每月的服务器，每月 1T 的流量如果只用来科学上网有点暴殄天物。还是多折腾下吧！



[Chevereto is an image hosting script that allows you to create a beautiful and full-featured image hosting website on your own server. It’s your hosting and your rules, say goodbye to closures and restrictions.](https://github.com/Chevereto/Chevereto-Free)

点击上面的文字可以跳转到 chevereto 的 github 页面，如果只是个人使用，免费版应该是足够的，而且搭建完成后可以在后台升级到收费版。（百度了下似乎也有盗版的存在，但是不推荐，如果因为使用盗版被通知服务器运营商封了你的服务器就得不偿失了）

下面是搭建流程：

### 1. 环境配置

在 chevereto 的 github 页面上可以了解其服务器环境的基本要求：

- Apache / NGiNX web server
- PHP 5.5.0 (standard libraries)
- MySQL 5.0 (ALL PRIVILEGES)

我推荐直接一套 LAMP 走起，[LAMP 一键安装包](https://lamp.sh/install.html) LAMP 的默认网站根目录： /data/www/default

### 2. git 拉项目

```
cd /data/www/default
git clone https://github.com/Chevereto/Chevereto-Free.git
```

到这一步，chevereto 就部署完成，以我为例，图床链接为http://47.105.69.170/Chevereto-Free



### 3. 配置 chevereto

第一次打开网站，可能会提示：Chevereto can’t create the app/settings.php file. You must manually create this file.

这里我们只需要在 app/下创建一个 setting.php 的空白文件即可。

之后刷新网站就会出现配置引导界面。

也有可能提示读写权限不够，只需要去修改提示的文件夹的权限即可。（chevereto 的 debug 做的已经相当完善）

如果出现其他问题，且网站提示隐藏了错误，那是因为 chevereto 的 debug level 默认为 1，需要去提示 app/settings.php 中的 debug level，详情可见<https://chevereto.com/docs/debug>

如果一切正常，可见下图，不过一般是英文 数据库即之前配置 LAMP 时的选择，如果使用的 MariaDB 也是一样的（MySQL 和它是完全兼容的）

如果一切正常，可见下图，不过一般是英文 数据库即之前配置 LAMP 时的选择，如果使用的 MariaDB 也是一样的（MySQL 和它是完全兼容的）



注意网站模式，如果是个人模式，网站是只能指定一个账户使用的，社区模式类似论坛。 但这些包括是否开启注册，在网站后台即 dashboard（仪表盘）都是可以设置的。

### 4. 上传图片

chevereto 不仅可以创建相册管理图片，也可以设置是否公开 `最重要的是，他的Embed codes功能，可以非常方便的获取各种格式的URL`![73a5358d28073a768d7e713ca2a2b411.jpg](http://47.105.69.170/Chevereto-Free/images/2018/12/07/73a5358d28073a768d7e713ca2a2b411.jpg)

### 5. 图片压缩

如果你博客上所有的图片未经压缩，动辄几 MB 的页面肯定是不流畅的，放在图床上也很臃肿 这里推荐一个压缩图片的网站：<https://tinypng.com/> 主要还是免费方便，而且压缩效果不凡
