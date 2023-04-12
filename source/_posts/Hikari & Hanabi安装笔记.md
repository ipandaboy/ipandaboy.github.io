---
title: Hikari & Hanabi安装笔记
date: 2020-03-13 15:25:32
categories: iOS
tags: [iOS,逆向]
---

# [Hikari](https://github.com/HikariObfuscator/Hikari "Hikari")
## 安装
现在安装不用再自己去Build，只需要下载[pkg][1]安装即可

# [Hanabi](https://github.com/HikariObfuscator/Hanabi "Hanabi")
## 安装

1. 下载[Release][2]版，里面包含以下文件

   ```
   libLLVMHanabi.dylib
   libLLVMHanabiDeps.dylib
   libsubstitute.dylib
   ```
2. 复制这3个文件到编译器目录

   ```
   /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/
   ```
3. 按顺序执行命令

   ```shell
   sudo optool install -c load -p @executable_path/libLLVMHanabiDeps.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
   
   sudo optool install -c load -p @executable_path/libLLVMHanabi.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
   
   sudo optool install -c load -p @executable_path/libLLVMHanabiDeps.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/swiftc
   
   sudo optool install -c load -p @executable_path/libLLVMHanabi.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/swiftc
   ```
4. 如果不再使用，卸载命令

   ```shell
   sudo optool uninstall -p @executable_path/libLLVMHanabi.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
   
   sudo optool uninstall -p @executable_path/libLLVMHanabiDeps.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
   
   sudo optool uninstall -p @executable_path/libLLVMHanabi.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/swiftc
   
   sudo optool uninstall -p @executable_path/libLLVMHanabiDeps.dylib -t /Applications/Xcode10.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/swiftc
   ```
# 使用 Hikari & Hanabi

Hanabi跳过123，直接开启混淆选项

1. Hikari需要更改Toolchains，如果没有Hikari选项，就是没安装成功

   ```
   Xcode -> Toolchains -> Hikari 
   ```

![](/images/selectHikari.png)

2. Build Settings -> Enable Index-While-Building Functionality 设置为 NO
![](/images/EnableIndex-While-BuildingFunctionality.png)

3. 关闭编译优化，将所有 target 的 Optimization Level 改为 None
![](/images/OptimizationNone.png)

4. 开启需要的混淆选项，在 Other C Flags 里面加。

   ```
   -mllvm -enable-allobf 全部启用
   -mllvm -enable-bcfobf 启用伪控制流  
   -mllvm -enable-cffobf 启用控制流平坦化
   -mllvm -enable-splitobf 启用基本块分割  
   -mllvm -enable-subobf 启用指令替换  
   -mllvm -enable-acdobf 启用反class-dump  
   -mllvm -enable-indibran 启用基于寄存器的相对跳转  
   -mllvm -enable-strcry 启用字符串加密  
   -mllvm -enable-funcwra 启用函数封装
   ```

![](/images/FlagsSet.png)

5. 全部开启，容易造成体积增大，提交审核存在被拒的风险，可指定文件加密，添加以上选项

   ```
   Build Phases -> Compile Sources -> Complier Flags 
   ```

![](/images/ComplierFlags.png)



[1]:https://github.com/HikariObfuscator/Hikari/releases/download/20190327/HikariObfuscatorInstaller-2019.03.27.pkg
[2]:https://github.com/HikariObfuscator/Hanabi/releases/download/7.0%401b02aa%40LoaderV4/7.0@1b02aa@LoaderV4.zip

