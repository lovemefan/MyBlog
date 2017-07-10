---
title: UWP学习笔记 (一) 初识UWP
date: 2017-07-08 11:02:00
tags: [UWP,APP开发,学习笔记] 
---
** {{ title }}：** <Excerpt in index | 首页摘要>
认识UWP及开发前的一些准备
<!-- more -->
<The rest of contents | 余下全文>
## 什么是UWP
>UWP即Windows 10 中的Universal Windows Platform简称。即Windows通用应用平台，在Win 10 Mobile/Surface(Windows平板电脑）/PC/Xbox/HoloLens等平台上运行，uwp不同于传统pc上的exe应用也跟只适用于手机端的app有本质区别。它并不是为某一个终端而设计，而是可以在所有windows10设备上运行。
微软在MWC 2015上首次展示了Win10统一平台战略的“代表作”：Win10通用应用（Windows10 Universal App）平台。在Win10中，所有设备将会运行在一个统一的Windows10系统核心之上。这样的设计使得一款应用可以在所有Win10设备上运行，今后Win10手机、平板电脑、笔记本电脑、PC、Xbox，甚至是3D全息眼镜HoloLens、巨屏触控Surface Hub和物联网设备例如Raspberry Pi 2等都不再有界限。新的通用平台允许新类型的Windows10通用应用真正实现一次编写、一套业务逻辑和统一的用户界面。应用在统一的Win10商店中将只会有一个安装包，而它将适用于所有Win10设备。[1]  在 Windows 10 Insider Preview 中的 Universal Windows Platform (UWP)借助 Windows 10 UWP 将在 Windows 应用中更上一层楼。UWP 会根据不同的设备类型使用相应的自适应 UI 控件，并使用运行 Windows 10 Insider Preview 的所有设备上必须具有的通用 API 集。简单的说，uwp就是通用应用的意思可以在电脑端，手机端，或其他设备通用。不用分别为不同的平台设计不同的软件。即一个软件就可以通吃。这是微软为win10系统定制的趋势。微软声称不管是开发者，还是使用者，都省事。   --百度百科

首先来欣赏一下国内一些比较用心的UWP
**网易云音乐**
![网易云音乐](http://oskhhyaq3.bkt.clouddn.com/blog/170708/HJG2J760dA.png?imageslim)

**IT之家**
![IT之家](http://oskhhyaq3.bkt.clouddn.com/blog/170708/A65Aa9ECm6.png?imageslim)
### 如何获取UWP
* 1.从Window 应用商店获取。打开应用商店，搜索并选择下载。
* 2.[离线部署](https://www.windows10.pro/how-to-install-uwp-offline-packages)
## 开发准备
* 开发环境：Windows 10 +Visual Studio 2015/2017    这里说明必须是**Windows 10 **，其他不行。VS 2015及以上才支持UWP开发，所以只能用VS 2015或2017。我目前的环境是 Win10 创意者 + VS 2017。
* 开发者模式。前往 设置-更新与安全-针对开发者-开发者模式
* 技术储备 C#/C++/VB 后期我们将使用C#进行开发程序的逻辑部分 [C#微软官方教程（有中文字幕）](http://bit.do/csharp-fundamentals)
* XAML(EXtensible Application Markup Language)。XAML是一种类似HTML的标记语言。用来设计UI部分后面会着重学习XAML语言。如果是有HTML基础的同学会很容易上手。
## 总结
我对windows Phone有一种特有的情怀，从之前的Windows Phone 7 开始，我就喜欢Windows Phone上了其流畅顺滑的操作。到后来的Windows 10 mobile 。由于其软件生态太差，无法满足生活需求，我才不得不转向Android阵营。以前Android的卡慢是我无法忍受的，但随着Android 6.0/7.0，即将发布的Android 8.0，Android慢慢优化的系统也能适应大部分人的需求。Android，iOS是大势所趋，我为什么还要选择UWP这种有些人听都没听过的平台呢？
* 首先，我看重的是UWP的优势，一次编译，能在所有Win 10 设备运行，包括电脑、平板、手机(Win10 手机)、XBox、HoloLens、surface Hub、loT(物联网)。微软费尽心思推广Win10，就是为了增加UWP的运行环境。现在及未来Win10的装机量不容小视。而且UWP小巧轻便，前途无可限量。
* 其次，UWP有着自己的类似Google Play和Apple Store的应用商店，保证其安全性。
* 然后，我想尽自己一份微薄力量来完善Windows 生态，主要还是Windows phone的生态。
## 学习资料
* UWP微软官方学习课程 [官方MVA]]() [bilibili搬运](http://www.bilibili.com/video/av7997007/)
Microsoft Virtual Academy (MVA)   [【链接】](https://mva.microsoft.com/)是微软官方的一个免费的视频教学课堂。里面有大量的学习资源(有中文字幕)，强烈推荐。
* 深出浅入UWP （中文课程）[【bilibili】](http://www.bilibili.com/video/av3610677)