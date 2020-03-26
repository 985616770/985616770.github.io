---
title: ubuntu前端工具安装
tags:
- Ubuntu
- 入门
date: 2018-12-01 07:59:35
categories: 服务器
---

# ubuntu 前端工具安装

<!-- more -->

### 登入 vps

```shell
ssh -p port username@ip_address
```



### 安装 git

1. 首先更新 apt-get 的源,顺便升级已安装的软件，接着安装 git 包。

```shell
$ apt-get update
$ apt-get upgrade
$ apt-get install git
```

2. 给 manager 用户在服务器上生成一个 ssh 公钥和私钥
   `ssh-keygen`该命令会在用户根目录下创建.ssh 目录，并生成 id_rsa 和 id_rsa.pub 文件
3. 在本地机用户目录下的.ssh 文件夹内，启动命令行工具，将本地机的公钥保存到服务器上
   `ssh-copy-id manager@id_address -p [port]`这行命令会在远端 manager 目录下生成一个 authorized_keys 文件。
   `cat .ssh/authorized_keys`在 manager 的用户根目录中（/home/manager）用 cat 命令打印出该文件内容
4. 将服务器的 ssh 公钥保存到 github 上

### 安装 nvm 和 nodejs

1. 安装脚本

```shell
$ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

2. 使环境变量生效

   ```shell
    $ source .bashrc
   ```

3. 切换源

   ```shell
   $ NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
   ```

4. 安装 nodejs

   ```shell
   $ nvm install stable # 安装最新稳定版

   ```
