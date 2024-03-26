---
layout:       post
title:        "更改 Oracle Cloud 实例主机名"
author:       "ifeng"
header-style: text
catalog:      true
tags:
    - Oracle Cloud
    - Hostname
---
> 这篇文章转载自[小汐技术栈](https://tech.soraharu.com/archives/50/)

在使用 Oracle Cloud 实例服务的时候遇见了一个怪事，每次修改 hostname 一段时间后，都会自动变更回来，如何设置都无效，在查阅 Oracle Cloud 支持文档后终于解决了这个问题，在此做个记录。

1、修改 OCI Hostname 配置文件
```shell
vi /etc/oci-hostname.conf
```
将其中的 `PRESERVE_HOSTINFO=0` 修改为 `PRESERVE_HOSTINFO=1`

2、设置实例主机名
将 OracleCloud 更改为想要设置的主机名：
```shell
hostnamectl set-hostname OracleCloud
```
或者也可以直接在 Cockpit 上直接设置。
