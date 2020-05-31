---
title:      "让Ubuntu打开就是命令行界面"
cover:      "https://image.animekid.cn/images/2019/02/02/9dbee32ce1d723d0a7a4120e31480b48.md.jpg"
date:       "2019-02-01 14:14:37"
tags:
    - Linux Desktop
---

`sudo systemctl disable lightdm.service`首先停止登录界面的图形化。  
编辑`/etc/default/grub`文件，将其中的`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash`"后面的值换成 *text*，然后执行`sudo update-grub`，重启就行了。  
`[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx`添加到`.bashrc`中，代表的就是从终端登录之后执行startx启动图形化界面。
