---
title:      "Android Studio 运行AVD提示应用程序无法安装"
cover:      "https://image.123m.me/images/2019/02/02/53133e4d895d22dd8ae164b8cb68ff9a.png"
date:       "2019-02-26 11:34:20"
tags:
    - 开发工具
---

更改一个项目后，重新移动项目到别的文件夹。  
移动到新的文件夹后，却发现之前的项目运行不了，无法进行AVD测试

#### 解决办法
1. 清理之前打包的apk文件  
点击build->clean project ,然后再点击 rebuild project。
2. 然后运行AVD就可以将软件安装进去了