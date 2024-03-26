---
layout: post
title: "使用 RPM 命令升级 CentOS 7 操作系统内核"
subtitle: "Update Kernel in CentOS to the New Version"
author: "ifeng"
header-img: ""
header-bg-css: "linear-gradient(to right, #b0091a, #4b0208);"
tags:
  - CentOS
  - Kernel
---

　　在 CentOS 中，YUM 是一种包管理器，它允许用户在操作系统中安装、更新和删除软件包。YUM 提供了一种简单的方法来管理软件包的依赖性，并且它可以自动处理软件包之间的依赖关系。这使得安装和升级软件包变得更加容易，因为用户不需要手动解决软件包之间的依赖关系。我们在升级操作系统内核时，会经常用到 YUM 命令，连接远程的镜像源，自动处理依赖关系，完成内核软件包的安装。

　　提到镜像源（软件仓库），我们不得不说 Elrepo ，Elrepo.org 的创办人是 Stephen Rothwell 和 David Milburn。elrepo.org 作为一个第三方软件仓库，专注于为企业级 Linux 操作系统提供高质量、稳定的软件包和驱动程序，因此在这个领域有着很高的知名度和声誉。

　　半年前，我就为小伙伴分享了 [使用 YUM 升级 CentOS 操作系统内核](https://www.hicairo.com/post/48.html) 的方法，就在前几天，我在 Vultr.com 的 VPS 上调试一段程序，需要升级操作系统内核。

```shell
[root@vultr ~]# yum -y update
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.xtom.com
 * epel: opencolo.mm.fcix.net
 * extras: mirror.keystealth.org
 * updates: abqix.mm.fcix.net
No packages marked for update
[root@vultr ~]# rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
curl: (22) The requested URL returned error: 403 Forbidden
error: https://www.elrepo.org/RPM-GPG-KEY-elrepo.org: import read failed(2).
[root@vultr ~]#
```

　　提示 Elrepo 阻止访问他们的服务器，我使用本地浏览器访问 www.elrepo.org 一切正常，看来 Elrepo 的确屏蔽了  Vultr.com 数据中心的 IP 地址，原因我猜测可能是因为大量用户使用 Vultr.com 的 VPS，反复的连接 Elrepo 镜像源拉取软件包， Elrepo 认为这种一种滥用行为，从而进行了屏蔽。

　　既然不能使用 YUM 安装操作系统内核，那我们就回到最原始的状态，使用 RPM 命令来升级操作系统内核。

一、查询系统版本和内核版本
--

```shell
[root@vultr ~]# cat /etc/redhat-release
CentOS Linux release 7.9.2009 (Core)
[root@vultr ~]# uname -r
3.10.0-1160.83.1.el7.x86_64
```

　　从以上信息我们可以看出，我目前的操作系统版本为 CentOS Linux 7.9.2009 ，内核版本为 3.10.0-1160.83.1.el7.x86_64 ，其中，3.10.0 表示主版本号，1160.83.1.el7 表示发行版的特定版本号，x86_64 表示 CPU 架构。

二、手动下载内核软件包
--

　　打开 [https://elrepo.org/linux/kernel/](https://elrepo.org/linux/kernel/) ，手动下载对应版本的内核软件包并上传到服务器。例如我下载的是这两个文件：

```shell
# 注意，如果 elrepo.org 屏蔽了你的服务器 IP 地址，请将软件包下载到本地，再通过 WinSCP 等软件包上传到服务器，是不能通过 wget 命令直接下载的。
wget https://elrepo.org/linux/kernel/el7/x86_64/RPMS/kernel-ml-6.3.0-1.el7.elrepo.x86_64.rpm
wget https://elrepo.org/linux/kernel/el7/x86_64/RPMS/kernel-ml-devel-6.3.0-1.el7.elrepo.x86_64.rpm
```

三、安装 rpm 包
--

```shell
rpm -ivh kernel-ml-6.3.0-1.el7.elrepo.x86_64.rpm
rpm -ivh kernel-ml-devel-6.3.0-1.el7.elrepo.x86_64.rpm
```

四、修改 GRUB 中默认的内核版本
--

1、内核升级完毕后，目前内核还是默认的版本，如果此时直接执行 `reboot` 命令，重启后使用的内核版本还是默认的 `3.10.0`，不会使用新的 `6.3.0` ，首先，我们可以通过命令查看默认启动顺序

```shell
[root@vultr ~]# awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
0 : CentOS Linux (6.3.0-1.el7.elrepo.x86_64) 7 (Core)
1 : CentOS Linux 7 Rescue 853360358a904d2196a5f00ef85dfa7a (3.10.0-1160.88.1.el7.x86_64)
2 : CentOS Linux (3.10.0-1160.88.1.el7.x86_64) 7 (Core)
3 : CentOS Linux (3.10.0-1160.83.1.el7.x86_64) 7 (Core)
4 : CentOS Linux (3.10.0-1160.el7.x86_64) 7 (Core)
5 : CentOS Linux (0-rescue-8007323efcc84eed8641e3343df5577b) 7 (Core)
```

2、由以上信息可以看出新内核(6.3.0)目前位置在 0，原来的内核(3.10.0)目前位置在 1，所以如果想生效最新的内核，还需要我们修改内核的启动顺序为 0

```shell
[root@vultr ~]# grub2-set-default 0
```

3、运行 `grub2-mkconfig` 命令来重新创建内核配置

```shell
[root@vultr ~]# grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-6.3.0-1.el7.elrepo.x86_64
Found initrd image: /boot/initramfs-6.3.0-1.el7.elrepo.x86_64.img
Found linux image: /boot/vmlinuz-3.10.0-1160.88.1.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-1160.88.1.el7.x86_64.img
Found linux image: /boot/vmlinuz-3.10.0-1160.83.1.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-1160.83.1.el7.x86_64.img
Found linux image: /boot/vmlinuz-3.10.0-1160.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-1160.el7.x86_64.img
Found linux image: /boot/vmlinuz-0-rescue-853360358a904d2196a5f00ef85dfa7a
Found initrd image: /boot/initramfs-0-rescue-853360358a904d2196a5f00ef85dfa7a.img
Found linux image: /boot/vmlinuz-0-rescue-8007323efcc84eed8641e3343df5577b
Found initrd image: /boot/initramfs-0-rescue-8007323efcc84eed8641e3343df5577b.img
done
```

五、使用 reboot 命令重启后，查看内核版本
--

```shell
[root@vultr ~]# reboot
[root@vultr ~]# uname -r
6.3.0-1.el7.elrepo.x86_64
```
