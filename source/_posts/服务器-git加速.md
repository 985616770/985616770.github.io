---
title: 各种代理加速
tags:
- git
date: 2019-12-01 07:59:35
categories: 服务器
---
<!-- more -->

# 针对 github.com

## http / https协议

>  命令行中输入

设置 Git 全局代理的命令如下：

```shell
$ git config --global http.https://github.com.proxy http://127.0.0.1:8889
$ git config --global https.https://github.com.proxy http://127.0.0.1:8889
# 取消当前使用代理
$ git config --global --unset http.proxy
# 查看当前使用代理
$ git config -l
$ git config --global --get http.proxy

```



## ssh/git

>  修改~/.ssh/config文件

```shell
ProxyCommand connect -S 127.0.0.1:8080 %h %p 
# proxy hostname:port
# 这个地方会针对全局的git 注意!!

Host github.com
  User git
  Port 22
  Hostname github.com
  IdentityFile "C:\Users\98561\.ssh\id_rsa" # path
  TCPKeepAlive yes
  IdentitiesOnly yes

Host ssh.github.com
  User git
  Port 443
  Hostname ssh.github.com
  IdentityFile "C:\Users\98561\.ssh\id_rsa" # path
  TCPKeepAlive yes
  IdentitiesOnly yes
```



(set the correct **proxy hostname:port,** and **the path to id_rsa**. When you use git-bash, use slashes in the path to id_rsa)

设置`正确的代理服务器,端口`

和`私钥` 的`正确位置`

## yarn加速

```shell
yarn config set proxy http://127.0.0.1:8889
yarn config set https-proxy http://127.0.0.1:8889

# 配置国内镜像-淘宝镜像
yarn config set registry https://registry.npm.taobao.org
```

淘宝源的速度快些

## npm

```shell
npm config set proxy http://127.0.0.1:8889
npm config set https-proxy http://127.0.0.1:8889

npm config set registry http://registry.npm.taobao.org

```

## 注意如果你换成淘宝镜像的话，会影响你发布模块，这时候需要换回npm官网的镜像

```
npm config set registry https://registry.npmjs.org
```

