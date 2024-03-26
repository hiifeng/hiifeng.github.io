---
layout:     post
title:      "CentOS 7 防火墙详细配置"
subtitle:   "Detailed Configuration of CentOS 7 Firewall"
date:       2022-10-05
author:     "ifeng"
header-img: "img/post-bg-os-metro.jpg"
catalog: true
tags:
  - CentOS
  - Firewall 
---
> 这篇文章转载自 [HiFeng’Blog](https://www.hicairo.com/post/21.html) ,转载请保留链接 ;)

**1、查看防火墙状态**

```shell
systemctl status firewalld
```

**2、开启防火墙**

```shell
systemctl start firewalld
```

**3、关闭防火墙**

```shell
systemctl stop firewalld
```

**4、设置开机启动**

```shell
systemctl enable firewalld
```

**5、禁止开机启动**

```shell
systemctl disable firewalld
```

**6、查看防火墙配置**

```shell
firewall-cmd --state
firewall-cmd --list-all
```

**7、查询端口是否开放**

```shell
firewall-cmd --query-port=8080/tcp
```

**8、允许80端口访问**

```shell
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --reload    #重新加载防火墙配置才会起作用
```

**9、移除80端口**

```shell
firewall-cmd --permanent --remove-port=80/tcp
firewall-cmd --reload
```

**10、允许某个端口段**

```shell
firewall-cmd --permanent --zone=public --add-port=1000-2000/tcp
firewall-cmd --reload
```

**11、允许某个IP访问，默认允许**

```shell
firewall-cmd --permanent --add-rich-rule='rule family=ipv4 source address=192.168.1.169 accept'
firewall-cmd --reload
```

**12、禁止某个IP访问**

```shell
firewall-cmd --permanent --add-rich-rule='rule family=ipv4 source address=10.0.0.42 drop'
firewall-cmd --reload
```

**13、允许某个IP访问某个端口**

```shell
firewall-cmd --permanent --add-rich-rule='rule family=ipv4 source address=192.168.1.169 port protocol=tcp port=6379 accept'
firewall-cmd --reload
```

**14、移除以上规则**

```shell
firewall-cmd --permanent --remove-rich-rule='rule family="ipv4" source address="192.168.1.169" port port="6379" protocol="tcp" accept'
firewall-cmd --reload
```

**15、允许某个IP段访问**

```shell
firewall-cmd --permanent --add-rich-rule='rule family=ipv4 source address=10.0.0.0/24 accept'
```

**16、重启防火墙**

```shell
firewall-cmd --reload
```
