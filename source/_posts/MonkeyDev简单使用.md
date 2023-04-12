---
title: MonkeyDev简单使用
date: 2021-10-17 16:51:40
categories: iOS逆向从入门到放弃
tags: [iOS,逆向]
---

# 获取IPA包

出来混最重要的是什么？是出来。逆向App最重要的是什么？是App！！！

那么App哪里来呢？

1. 自己写的App，源代码编译出来的是没有加壳的，可以直接用来分析

2. App Store，TestFlight上的，需要砸壳，之前[一键砸壳](https://ipandaboy.github.io/2020/03/17/一键砸壳/)有详细介绍

3. 别人分享的ipa包，直接下载

4. 网站上的点击安装，实际就是下载一个plist文件，里面有指向ipa的地址



如何从第4种方式拿到我们所要的ipa包呢？？？

1.通过抓包形式

通过Charles或Thor抓到plist内容，查看ipa的实际地址

通过谷歌浏览器Chrome抓到plist内容，查看ipa实际地址

2.使用[IpaDownloadTool](https://github.com/SmileZXLee/IpaDownloadTool)下载ipa包



# MonkeyDev 

未安装MonkeyDev的请查看[Wiki](https://github.com/AloneMonkey/MonkeyDev/wiki)进行安装或者直接执行下面命令安装

```shell
sudo /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/AloneMonkey/MonkeyDev/master/bin/md-install)"
```

新建MonekyApp，把app包放到TargetApp文件夹里面，运行到真机上，就相当于重签了

![](/images/monekyDemo.png)

修改一下pch的路径，不修改也可以运行



首先我们从UI入手，打开Reveal，可以查看到运行的App

因为MonkeyDev用的```RevealServer.framework```不是最新的，最新版的Reveal无法查看App，需要替换，Reveal替换 ```/opt/MonkeyDev/Frameworks的RevealServer.framework```



查看我们要hook的界面是属于哪个界面, 是属于```NewMainFrameViewController```

那怎么写代码呢？看一下MonkeyApp的项目结构吧，此处省略几百字介绍，在[MonekDev](https://github.com/AloneMonkey/MonkeyDev/wiki)上都有，直接上[Demo]()

有个很好的功能，把MDConfig.plist里面的BaseMsgContentViewController改成我们的NewMainFrameViewController，再次运行一下，可以看到控制台输入很多东西，其他有viewDidLoad，说明他是执行过此函数，那我们在这个函数里面搞事吧

主要代码是写在testDylib.xm上，用logo的写法，需要把testDylib.xm的type改成Object-c

++ Source 才可以下断点调试，不建议在此写代码。

 ```objective-c
 %hook NewMainFrameViewController
 -(void)viewDidLoad{
     %orig;//执行之前的效果代码
     //HookCode
 }
 %end
 ```



改用Swizzed的方式，导入两个NSObject+HKMethodSwizzed.h，NSObject+HKMethodSwizzed.m就可以直接写Hook了

```objective-c
[NSObject hk_hookInstanceMethod:[NewMainFrameViewControllerHooker class] originalClass:NSClassFromString(@"NewMainFrameViewController") swizzledSelector:@selector(wxhk_viewDidLoad) originalSelector:@selector(viewDidLoad)];
```

```objective-c
-(void)wxhk_viewDidLoad{
    [self wxhk_viewDidLoad];//执行之前的效果代码
    //HookCode
}
```







