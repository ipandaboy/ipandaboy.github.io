---
title: Xcode环境简单部署笔记
date: 2020-03-13 14:25:56
categories: programming
tags: [iOS,逆向]
---

**Xcode被破坏，重装后需要安装一些环境，写个笔记记录一下，以后安装不用再去看各个Wiki**

1.安装最新版[theos](https://github.com/theos/theos/wiki/Installation "theos")，有安装直接跳过
```
sudo git clone --recursive https://github.com/theos/theos.git /opt/theos
```
2.重新安装[MonkeyDev](https://github.com/AloneMonkey/MonkeyDev/wiki "MonkeyDev")，Xcode打开，可以创建MonkeyApp了
```
sudo /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/AloneMonkey/MonkeyDev/master/bin/md-install)"
```

因为MonkeyDev用的RevealServer.framework不是最新的，最新版的Reveal无法查看App，需要替换，Reveal替换/opt/MonkeyDev/Frameworks的RevealServer.framework

3.安装[Hikari](https://github.com/HikariObfuscator/Hikari "Hikari")，下载[pkg][1]安装

张总还有一个[Hanabi](https://github.com/HikariObfuscator/Hanabi "Hanabi"),请看另外一篇




[1]:https://github.com/HikariObfuscator/Hikari/releases/download/20190327/HikariObfuscatorInstaller-2019.03.27.pkg
[2]:https://github.com/HikariObfuscator/Hanabi/releases/download/7.0%401b02aa%40LoaderV4/7.0@1b02aa@LoaderV4.zip