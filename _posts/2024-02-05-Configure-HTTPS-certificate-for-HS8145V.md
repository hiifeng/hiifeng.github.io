---
layout: post
title: "华为光猫 HS8145V 配置 Https（SSL）证书"
subtitle: "Configure HTTPS (SSL) certificate for HS8145V"
author: "ifeng"
header-img: "img/2024-02-05-bg.jpg"
header-mask: 0.5
tags:
  - 华为
  - HS8145V
  - Https证书
---

> 这篇文章转载自 [HiFeng'Blog](https://www.hicairo.com/post/18.html),转载请保留链接 ;)

　　华为的光猫稳定性一直很不错，配置好扔到弱电箱，基本可以无视它的存在。对于普通家庭，网络结构越简单越好，将光猫配置为 Router 模式进行工作，手机、笔记本电脑、Tv机顶盒等终端设备连接光猫的Wifi热点进行数据传输，是很多家庭的选择。

　　同时，在光猫中配置 DDns ，可以实现光猫的远程管理。但是有些资深玩家或技术控总是感觉通过 http 协议传输不完美，接下来就为大家介绍如何实现通过 Https 方式访问光猫。

　　该方法已经在 Hs8145v/固件版本V3R017C10S118 上测试通过，华为其他型号的应该也差不多，有问题欢迎留言或进入Tg群组（[https://t.me/HiaiFeng](https://t.me/HiaiFeng)）进行交流。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664675783737142.webp)

1、为自己绑定光猫 DDns 的域名申请一个 SSL 证书。

目前提供免费 SSL 证书申请的机构很多，例如 Let's Encrypt 支持泛域名证书，但是有效期只有 3 个月，到期前需要再次申请，于是笔者选择在 DnsPod 上申请 1 年的免费证书。

登录 Dnspod SSL 证书控制台，点击“申请免费证书”。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664675854279404.webp)

选择申请免费版证书。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664675934428850.webp)

填入相关信息，“域名验证方式”根据情况自行选择，然后点击更多。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664675953185287.webp)

`务必设置私钥密码，并记住`。接下来会用到。然后点击“提交申请，进行域名验证”按钮。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664676004634140.webp)

根据系统提示，验证域名后，点击“完成”按钮。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664676025102944.webp)

系统进入证书列表，查看你申请证书的状态，可能需要等几分钟。当状态变为“已签发”，点击“下载”按钮。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664676131798429.webp)

选择服务器类型是Apache的证书进行下载。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664676149174114.webp)

2、为Hs8145v安装SSL证书

我们会得到一个 hicairo.tk_apache.zip（Your domain name_apache.zip）文件，将文件解压后有四个文件，分别是 hicairo.tk.crt、hicairo.tk.csr、hicairo.tk.key 和 root_bundle.crt 。使用 Notepad+ 新建一个 hicairo.tk.pem 文件，依次将 hicairo.tk.key、root_bundle.crt、hicairo.tk.crt 文件内容 copy 到 hicairo.tk.pem 文件里。

hicairo.tk.pem的文件格式如下：

```shell
#-----BEGIN RSA PRIVATE KEY-----
#这部分是（hicairo.tk.key）文件的内容
#-----END RSA PRIVATE KEY-----
##-----BEGIN CERTIFICATE-----
##这部分是（root_bundle.crt）文件的内容
##-----END CERTIFICATE-----
#-----BEGIN CERTIFICATE-----
#这部分是（hicairo.tk.crt）文件的内容
#-----END CERTIFICATE-----
```

然后登录光猫管理页面，在“系统工具 -> 修改登录密码”里，选中“能使证书认证”，填入密码（密码为申请SSL证书时填入的私钥密码，然后点击“应用”；最后导入刚才生成的证书文件（hicairo.tk.pem）后，重启光猫。

![](https://www.hicairo.com/zb_users/upload/2022/10/202210021664676171311898.webp)
