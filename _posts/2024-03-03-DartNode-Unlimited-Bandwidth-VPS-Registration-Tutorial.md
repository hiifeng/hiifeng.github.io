---
layout: post
title: "DartNode 无限流量 vps 注册申请教程"
subtitle: "DartNode Unlimited Bandwidth VPS Registration Tutorial"
author: "ifeng"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - VPS
  - DartNode
  - 不限流量
---

> 这篇文章转载自 [HiFeng'Blog](https://www.hicairo.com/post/71.html)

[DartNode](https://dartnode.com/?via=ifeng) 成立于 2023年，总部位于休斯顿技术中心的中心地带，是 Snaju® Inc. 的一个部门，在 NASA 约翰逊航天中心附近运营着一个 24/7/365 网络运营中心。DartNode 提供`带宽  1 Gb/s 不限流量的 vps 套餐`，其中 VPS-1 Plan `每月仅需 2 美元`，对于经常看 Netflix、youtube 或需要大量下载的小伙伴，终于不用担心流量用超的问题了。

## 一、测试 vps 速度

经过我一个多月的试用，vps 运行基本稳定，晚高峰时速度还比较理想，我使用的是电信 200M 宽带，以下为直连的测速情况。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454179545169.webp)

以下为使用 hysteria2 协议的测速情况，可以跑满我的宽带。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454193313677.webp)

以下是使用 Bench.sh 的检测情况，其中包含服务器硬件配置信息、 I/O 速度、与各个国家/地区的网速情况。虽然 DartNode 在其官网说明提供带宽为  1 Gb/s 不限流量套餐，但从以下的测试结果来看，并没有达到 1 Gb/s 的速度，但是我感觉 200-300 Mb/s 的速度也基本可以满足日常工作和学习的需求。
```shell
-------------------- A Bench.sh Script By Teddysun -------------------
 Version            : v2023-10-15
 Usage              : wget -qO- bench.sh | bash
----------------------------------------------------------------------
 CPU Model          : Intel(R) Xeon(R) CPU E5-2697 v2 @ 2.70GHz
 CPU Cores          : 1 @ 2699.998 MHz
 CPU Cache          : 16384 KB
 AES-NI             : ✓ Enabled
 VM-x/AMD-V         : ✗ Disabled
 Total Disk         : 10.0 GB (2.4 GB Used)
 Total Mem          : 974.7 MB (315.7 MB Used)
 System uptime      : 37 days, 21 hour 45 min
 Load average       : 0.05, 0.07, 0.02
 OS                 : CentOS Linux release 7.9.2009 (Core)
 Arch               : x86_64 (64 Bit)
 Kernel             : 6.7.1-1.el7.elrepo.x86_64
 TCP CC             : cubic
 Virtualization     : KVM
 IPv4/IPv6          : ✓ Online / ✓ Online
 Organization       : AS399646 Snaju Development
 Location           : Houston / US
 Region             : Texas
----------------------------------------------------------------------
 I/O Speed(1st run) : 85.4 MB/s
 I/O Speed(2nd run) : 71.0 MB/s
 I/O Speed(3rd run) : 81.5 MB/s
 I/O Speed(average) : 79.3 MB/s
----------------------------------------------------------------------
 Node Name        Upload Speed      Download Speed      Latency
 Speedtest.net    337.18 Mbps       619.38 Mbps         18.19 ms
 Los Angeles, US  257.40 Mbps       371.00 Mbps         37.94 ms
 Dallas, US       462.26 Mbps       374.00 Mbps         8.31 ms
 Montreal, CA     587.50 Mbps       677.16 Mbps         48.13 ms
 Paris, FR        76.74 Mbps        454.88 Mbps         113.21 ms
 Amsterdam, NL    224.56 Mbps       791.66 Mbps         116.42 ms
 Shanghai, CN     185.50 Mbps       924.59 Mbps         193.23 ms
 Hongkong, CN     187.20 Mbps       65.38 Mbps          217.23 ms
 Mumbai, IN       24.22 Mbps        233.17 Mbps         254.74 ms
 Singapore, SG    97.70 Mbps        551.87 Mbps         207.44 ms
 Tokyo, JP        76.76 Mbps        354.08 Mbps         136.26 ms
----------------------------------------------------------------------
 Finished in        : 6 min 45 sec
 Timestamp          : 2024-03-01 01:42:00 UTC
----------------------------------------------------------------------
```

## 二、账号注册

1、打开如下网址，点击屏幕右上角的“Dashboard”按钮。

[https://dartnode.com/?via=ifeng](https://dartnode.com/?via=ifeng)

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454291702729.webp)

2、如图所示，点击“Join Today”。当然如果你有 Gmail 邮箱，也可以选择“Sign with in Google”。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454369800314.webp)

3、如图所示，输入相关信息后，点击“Join Today”按钮。由于 DartNode 在注册过程中，不验证信息的真实性，请确认邮箱是否输入正确，在忘记密码时，邮箱是取回密码的唯一凭证。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454386275132.webp)

4、这时会自动登录，跳转至如下页面，然后点击页面右上角你的用户名中的“Settings”。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454409770083.webp)

5、输入个人信息后点击页面底部的“>>Save && Update”按钮。请注意，Phone Number 请输入真实的号码，Google voice 号码也可以。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454433135281.webp)

## 三、开通 vps 套餐

1、如图所示，点击“Cloud Services”中的“Cloud VPS”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454454504012.webp)

2、如图所示，点击“Provision New Server”按钮，创建 VPS。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454470669758.webp)

3、如图所示，选择适合自己的 vps 套餐，然后点击“Order Today”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454485191357.webp)

4、如图所示，填写 Hostname ，选择操作系统后，点击右下角的“Continue”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454499896460.webp)

5、如图所示，选择 DDOS 防护设置、自动备份设置、IP 设置后，点击右下角的“Continue”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454630872276.webp)

6、如图所示，点击“Order Now”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454648310080.webp)

7、DartNode 支持多种付款方式，我们选择使用支付宝进行付款，如图所示，点击右下角的“Reload & Pay $***”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454669978230.webp)

8、选择“支付宝”后点击“支付”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454694352912.webp)

9、这时页面跳转至支付宝收银台，使用手机扫描二维码完成支付即可。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454710252499.webp)

## 四、管理自己的 vps

1、点击顶部菜单“Cloud Services”中的“Cloud VPS”后，你会看到你的 vps，如图所示，点击你的 vps 。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454836466497.webp)

2、这时，你将看到你的 vps 的相关信息，包含 IP 地址、root 用户密码等，在这个页面你可以设置反向 DNS 解析，重装操作系统等。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454854890217.webp)

## 五、DartNode 账户充值

DartNode vps 是按月进行计费的，如果您没有绑定信用卡，建议给 DartNode 充值一些费用，避免 vps 到期后忘记充值带来不必要的麻烦。

1、点击页面顶部的“Biling”按钮，然后点击页面右侧的“Reload Account Balance”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454884676053.webp)

2、DartNode 支持每次最低充值 5 美元，选择充值金额后，点击“Reload With Stripe”按钮。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454902598990.webp)

3、这时页面再次跳转至 Stripe 的页面，选择“支付宝”后点击“支付”按钮，按照提示完成充值即可。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454917439324.webp)

## 六、有关 DartNode vps 的一些说明

1、DartNode 的介绍中提到，vps的出口带宽为 1 Gb/s ，但是在我的实际测试过程中，并没有达到 1 Gb/s 的速度，从本文第一章节可以看到有关测速的详细情况。目前的这个速度基本上也可以满足工作和学习的需要，我感觉性价比还是可以的。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454936396565.webp)

2、 DartNode vps 提供的是不限流量套餐，但是在相关描述中提到“`我们不限制或计量我们服务器的带宽，您每月可以使用大量带宽，只要它符合我们的可接受使用政策。`”，有关符合 DartNode 可接受的政策，我也咨询了 DartNode 的客服人员，是否会因为 vps 占用 CPU 资源过高或流量使用过多而终止服务，对方的回复是他们并没有因为CPU使用率或带宽而取消任何服务，该政策是针对严重滥用行为的包罗万象。如果 DartNode 的带宽接近容量，他们会进行设备或网络的升级。因此目前来看，我认为是可以放心使用的。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454955808154.webp)

以下为 DartNode 客服的回复截图。

![](https://www.hicairo.com/zb_users/upload/2024/03/202403031709454973613054.webp)
