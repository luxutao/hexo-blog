---
title:      "virtualbox安装macos"
cover:      "https://image.123m.me/images/2019/02/02/8c4ecc84c25361cca5b2e12a6ef6d405.png"
date:       "2019-08-03 13:00:57"
tags:
    - VirtualBox
---

1. 安装virtualbox  
[Virtualbox官方下载](https://www.virtualbox.org/wiki/Downloads)  
2. 下载封装的vmdk文件  
[MacOS 10.12](https://drive.google.com/file/d/0Bx7BAMlD-ZOQTEpoVTF0Q0NpOVU/view?usp=sharing)  
[MacOS 10.13.6](https://drive.google.com/file/d/1LvnciaiQ6wbKoLzi46Usv1NU5mh6DwBG/view?usp=drive_open)  
3. 新建虚拟机  
    * 打开 VirtualBox 新建虚拟电脑
    * 命名 MacOS
    * 选择类型为 Mac OS X
    * 选择版本（我的是Mac OS X（64-bit））
    * 设置内存大小（4096MB）
    * 设置CPU数量及显存大小
    * 选择虚拟磁盘为刚刚下载的vmdk文件
4. 使用命令行打开virtualbox目录或linux直接执行该命令  
```shell
VBoxManage.exe modifyvm MacOS --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff

VBoxManage setextradata MacOS "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"

VBoxManage setextradata MacOS "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"

VBoxManage setextradata MacOS "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"

VBoxManage setextradata MacOS "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"

VBoxManage setextradata MacOS "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1

# 修改屏幕分辨率为 1440 * 900
VBoxManage setextradata MacOS VBoxInternal2/EfiGopMode 4

# VirtualBox5.2版本修改分辨率命令
VBoxManage setextradata MacOS VBoxInternal2/EfiGraphicsResolution 1440x900
```
5. 关闭启动刚刚创建的macos即可