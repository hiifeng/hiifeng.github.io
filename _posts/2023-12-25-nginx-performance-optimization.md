---
layout: post
title: "提升 Nginx TLS/SSL HTTPS 性能的 7 条优化建议"
subtitle: "7 Tips to Boost Nginx TLS/SSL HTTPS Performance"
author: "ifeng"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - Nginx
  - TLS
  - SSL
  - HTTPS
---

> 这篇文章转载自 [HiFeng'Blog](https://www.hicairo.com/post/68.html)，转载请保留链接 ;)

　　自 2018 年 7 月起，谷歌浏览器开始将 “HTTP” 网站标记为“不安全”。在过去的几年中，互联网已经迅速过渡到 HTTPS ，Chrome 浏览器的流量超过 70％，并且Web排名前100位的网站中有80多个现在默认使用HTTPS,当前Nginx作为最常见的服务器，广泛用于负载均衡（LB)、网关、反向代理。考虑到这一点，让我们看一下Nginx调优技巧，改善 Nginx + HTTPS 的性能以获得更好的 TTFB 和更少的延迟。

![](https://www.hicairo.com/zb_users/upload/2022/12/202212091670554430431871.webp)

**1. 开启 HTTP/2**

HTTP/2 最初是在 Nginx 版本 1.9.5中 实现的，以取代 spdy。在 Nginx 上启用 HTTP/2 模块很简单。

原先的配置：

```nginx
listen 443 ssl;
```
修改为：
```nginx
listen 443 ssl http2;
```
可以通过 curl 来验证：
```nginx
curl --http2 -I https://domain.com/
```
**2. 开启 SSL session 缓存**

启用 SSL Session 缓存可以减少 TLS 的反复验证，减少 TLS 握手。1M 的内存就可以缓存 4000 个连接，非常划算，现在内存便宜，尽量开启。
```nginx
ssl_session_cache shared:SSL:50m; # 1m 4000个，
ssl_session_timeout 1h; # 1小时过期 1 hour during which sessions can be re-used.
```
**3. 禁用 SSL session tickets**

由于 Nginx 中尚未实现 SSL session tickets，可以关闭。
```nginx
ssl_session_tickets off;
```
**4. 禁用 TLS version 1.0**

1.3 已经出来，1.0 可以丢进历史垃圾堆。
```nginx
ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;
```
修改为
```nginx
ssl_protocols TLSv1.2 TLSv1.3;
```
**5. 启用 OCSP Stapling**

如果不启用 OCSP Stapling 的话，在用户连接你的服务器的时候，需要去验证证书，这个验证证书的时间不可控，我们开启OCSP Stapling后，可以省掉这一步。
```nginx
ssl_stapling on;
ssl_stapling_verify on;
ssl_trusted_certificate /path/to/full_chain.pem;
resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 5s;
```
**6. 减小 ssl buffer size**

ssl_buffer_size 控制在发送数据时的 buffer 大小，默认情况下，缓冲区设置为 16k，为了最大程度地减少 TTFB（至第一个字节的时间），最好使用较小的值，这样 TTFB 可以节省大约30 – 50ms。
```nginx
ssl_buffer_size 4k;
```
**7. 调整 Cipher 优先级**

更新更快的 Cipher 放前面，这样延迟更小。
```nginx
# 手动启用 cipher 列表
ssl_prefer_server_ciphers on;  # prefer a list of ciphers to prevent old and slow ciphers
ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
```
