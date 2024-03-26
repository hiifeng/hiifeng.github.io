---
layout: post
title: "电视家等网络直播 APP 被禁用下架，免费看 IPTV 的解决办法"
subtitle: "How to watch TV for free in China"
author: "ifeng"
header-img: "img/post-bg-tv.png"
header-mask: 0.4
tags:
  - IPTV
  - 直播源
  - 流媒体播放器
---

> 这篇文章转载自[HiFeng'Blog](https://www.hicairo.com/post/68.html)


　　前不久广电总局要求年底实现开机就能看电视直播，本以为是一件利民惠民的好事呢，终于在11月20日晚上真相大白了，电视家等网络直播APP全部被禁用下架，想一年6-70元看直播不会再有了，还是老老实实一个月25元看有线电视吧，当然，你也可以选择不看电视。

　　最近国内社交平台有关看电视的话题吵的沸沸扬扬，我也很多年没有看过电视了，家里的电视基本就是摆设，本不想蹭这个热度的，结果前几天家里老人打电话告诉我，电视也不能看了。每个月给广电交25元虽然不多，但是总觉得不爽，不知道从什么时间开始，看个破电视也要收费了，儿时好像每家每户屋顶上都会架一个天线，遇到刮风时，电视上全是雪花点，这样也就出现了《我和我的祖国》中坊间邻居为了看女排比赛，小冬冬必须在自家屋顶不停的摆弄天线，那时的电视为我们带来了许多美好的儿时记忆。

　　电视家、火星直播等APP下架后，目前仍有一些APP可以正常使用，例如紫薇直播、海星直播等，但是法网恢恢，疏而不漏，我感觉随着时间的推移，肯定也会陆续下架。我为大家推荐的方案是，**在机顶盒/电视上安装流媒体播放器，流媒体播放器的节目接口调用自己WEB服务器中的接口文件，这样做的优点是，当节目源失效，更新WEB服务器上的接口文件后即可恢复正常，不用开车回家在机顶盒上进行相关设置。**

## 一、流媒体播放器

　　流媒体播放器有很多，例如TiviMate、IPTV Pro、mtv等，我推荐大家使用TiviMate。但是如果你使用中兴B860A、华为EC6108等早期的机顶盒，刷了当贝桌面，往往因为固件Android版本太低（很多固件的Android版本为4.x），不能安装TiviMate时，我推荐你使用一个名叫mtv的流媒体播放器。

TiviMate 2.1.5下载地址：

[https://github.com/hiifeng/IPTV/raw/main/player/TiviMate/TiviMate-2.1.5.apk](https://github.com/hiifeng/IPTV/raw/main/player/TiviMate/TiviMate-2.1.5.apk)

mtv下载地址：

[https://github.com/hiifeng/IPTV/raw/main/player/mtv/mtv.apk](https://github.com/hiifeng/IPTV/raw/main/player/mtv/mtv.apk)

其他流媒体播放器请在我的Github项目中查找下载：

[https://github.com/hiifeng/IPTV](https://github.com/hiifeng/IPTV)

## 二、节目源与流媒体播放器接口设置


### 1、节目源

　　节目源网上有许多，目前IPV6的节目源连接速度快且清晰稳定。如果打击力度持续加重，网络上分享的源越来越少，也可以自己抓源，YouTube上有很多抓源教程，就不展开赘述了。在此推荐两个节目源GitHub项目，首先对作者的付出表示感谢，大家可以去下载使用。有关节目源和直播软件的话题，也欢迎你在 telegram 群里（[https://t.me/HiaiFeng](https://t.me/HiaiFeng)）和大家讨论分享。

（1）范明明的节目源项目

[https://github.com/fanmingming/live](https://github.com/fanmingming/live)

（2）APTV项目的节目源

[https://github.com/Kimentanm/aptv](https://github.com/Kimentanm/aptv)

### 2、节目源的文件格式

　　TiviMate使用m3u格式的节目源文件，mtv使用txt格式的节目源文件。

m3u格式文件示例：
```shell
#EXTM3U x-tvg-url="https://www.hicairo.com/e.xml"
#EXTINF:-1 tvg-id="CCTV1" tvg-name="CCTV1" tvg-logo="https://www.hicairo.com/tv/CCTV1.png" group-title="央视频道",CCTV-1 综合
http://www.hicairo.com/3221227600/index.m3u8
http://live.hicairo.com/cctv1/index.m3u8
#EXTINF:-1 tvg-id="CCTV2" tvg-name="CCTV2" tvg-logo="https://www.hicairo.com/tv/CCTV2.png" group-title="央视频道",CCTV-2 财经
http://www.hicairo.com/3221227601/index.m3u8
#EXTINF:-1 tvg-id="北京卫视" tvg-name="北京卫视" tvg-logo="https://www.hicairo.com/tv/北京卫视.png" group-title="卫视频道",北京卫视
http://www.hicairo.com/3221227602/index.m3u8
#EXTINF:-1 tvg-id="湖南卫视" tvg-name="湖南卫视" tvg-logo="https://www.hicairo.com/tv/湖南卫视.png" group-title="卫视频道",湖南卫视
http://www.hicairo.com/3221227603/index.m3u8
#EXTINF:-1 tvg-id="NEWTV家庭剧场" tvg-name="NEWTV家庭剧场" tvg-logo="https://www.hicairo.com/tv/NEWTV家庭剧场.png" group-title="NewTV系列",家庭剧场
http://www.hicairo.com/3221227604/index.m3u8
#EXTINF:-1 tvg-id="NEWTV精品大剧" tvg-name="NEWTV精品大剧" tvg-logo="https://www.hicairo.com/tv/NEWTV精品大剧.png" group-title="NewTV系列",精品大剧
http://www.hicairo.com/3221227605/index.m3u8
```
txt格式文件示例：
```shell
央视频道,#genre#
CCTV-1 综合,http://www.hicairo.com/3221227600/index.m3u8
CCTV-1 综合,http://live.hicairo.com/cctv1/index.m3u8
CCTV-2 财经,http://www.hicairo.com/3221227601/index.m3u8
卫视频道,#genre#
北京卫视,http://www.hicairo.com/3221227602/index.m3u8
湖南卫视,http://www.hicairo.com/3221227603/index.m3u8
NewTV系列,#genre#
家庭剧场,http://www.hicairo.com/3221227604/index.m3u8
精品大剧,http://www.hicairo.com/3221227605/index.m3u8
```
### 3、将下载的节目源文件上传到自己的WEB服务器

　　将下载的节目源文件，参考上述节目源文件格式，经过编辑后上传到自己的WEB服务器供后续调用。编辑的目的是多源合并，如果某一个源失效，在使用机顶盒看直播时，可以自动切换到下一个源，例如示例文件中CCTV-1定义了两个直播源。将节目源上传到自己WEB服务器的目的，是为了解决源文件失效后，直接更新WEB服务器上的源文件即可，如果没有和老人在一起居住，不用开车回家在机顶盒上进行相关设置。

　　例如我的源文件为https://www.hicairo.com/iptv.m3u和https://www.hicairo.com/iptv.txt。

### 4、机顶盒中的流媒体播放器设置
**（1）TiviMate**

TiviMate安装完成后，首次启动的界面如下，使用遥控器点击“添加节目列表”按钮；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075182720057.webp)

输入节目列表地址，例如我的节目列表为 https://www.hicairo.com/iptv.m3u，输入完成并检查无误后，使用遥控器点击“下一个”按钮；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075198326739.webp)

这时会出现节目列表处理完成界面，使用遥控器点击“下一个”按钮；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075217987893.webp)

这时会出现节目预告源地址界面，使用遥控器点击“完成”按钮；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075233391165.webp)

这时就出现直播画面了。

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075249705747.webp)

TiviMate支持软件启动时更新节目列表，你可以通过遥控器在设置中看到相关设置，这样当你更新WEB服务器上的源文件后，老人在家重新启动一次机顶盒，失效的节目就恢复正常了。

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075267919377.webp)

**（2）mtv**

mtv流媒体播放器的启动界面如下；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075282856305.webp)

首次启动mtv后，由于软件中不包含任何节目源，会出现黑屏状态，这时按遥控器上的“菜单”按钮，调出设置菜单，按上下左右键，选择“接口设置”中的“节目地址”；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075295335928.webp)

输入节目列表接口，例如我的节目列表接口为https://www.hicairo.com/iptv.txt，输入完成并检查无误后，使用遥控器点击“确定”按钮；

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075309744407.webp)

这时就出现直播画面了。

![](https://www.hicairo.com/zb_users/upload/2023/11/202311271701075327454440.webp)

mtv同样也支持软件启动时更新节目列表，当你更新WEB服务器上的源文件后，老人在家重新启动一次机顶盒，失效的节目就会恢复正常。

## 参考

1.  范明明的节目源项目 [https://github.com/fanmingming/live](https://github.com/fanmingming/live)
2.  APTV项目的节目源 [https://github.com/Kimentanm/aptv](https://github.com/Kimentanm/aptv)
