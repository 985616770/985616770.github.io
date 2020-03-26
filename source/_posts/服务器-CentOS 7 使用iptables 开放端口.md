---
title: CentOS 7 使用iptables 开放端口
date: 2018-12-03 17:39:48
tags:
    - VPS
    - 服务器
    - CentOS
categories: 服务器
---

CentOS 7.0 默认使用的是 firewall 作为防火墙，这里改为 iptables 防火墙。

<!-- more -->

1、关闭 firewall：

```

systemctl stop firewalld.service

systemctl disable firewalld.service

systemctl mask firewalld.service

```


2、安装 iptables 防火墙

`yum install iptables-services -y`

3.启动设置防火墙

`\# systemctl enable iptables`

`\# systemctl start iptables`

4.查看防火墙状态

`systemctl status iptables`

5 编辑防火墙，增加端口

```
vi /etc/sysconfig/iptables #编辑防火墙配置文件

-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT

-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT

-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT

:wq! #保存退出
```

3.重启配置，**重启系统**

```
systemctl restart iptables.service #重启防火墙使配置生效

systemctl enable iptables.service #设置防火墙开机启动
```

4. 完整的防火墙配置信息

```
[root@izm5e11fdcw9aa5w6w9mm2z ~]# more /etc/sysconfig/iptables
\# sample configuration for iptables service
\# you can edit this manually or use system-config-firewall
\# please do not ask us to add additional ports/services to this default configuration
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```

5.注意开放端口的配置位置在**icmp-host-prohibited**这一行上面。
