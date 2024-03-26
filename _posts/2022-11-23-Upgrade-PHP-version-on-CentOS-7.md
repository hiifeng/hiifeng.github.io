---
layout:       post
title: "CentOS 7 升级 php 5.4 到 php 7.2"
subtitle: "Upgrade PHP version on CentOS 7"
author: "ifeng"
header-img: ""
header-bg-css: "linear-gradient(to right, #298E66, #035435);"
tags:
    - CentOS
    - php
---
> 这篇文章转载自 [HiFeng’Blog](https://www.hicairo.com/post/44.html) ,转载请保留链接 ;)

**原因：**

CentOS 7 下 yum 安装 php 版本默认是 5.4 的，但新框架要求 php 版本在 7 以上，所以把 php 升级一下了。

**查看yum的可安装的php版本列表：**

```shell
yum provides php
```

**开始升级PHP更新源：**

```shell
rpm -Uvh https://mirror.webtatic.com/yum/el7/epel-release.rpm 
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
yum remove php-common -y  
yum install -y php72w php72w-opcache php72w-xml php72w-mcrypt php72w-gd php72w-devel php72w-mysql php72w-intl php72w-mbstring
```

**查看版本：**

```shell
php -v
PHP 7.2.14 (cli) (built: Jan 12 2019 12:47:33) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.14, Copyright (c) 1999-2018, by Zend Technologies
```

**安装 php fpm：**

```shell
yum install php72w-fpm
#启动php-fpm
systemctl start php-fpm.service
#设置开机启动php-fpm
systemctl enable php-fpm.service
```
