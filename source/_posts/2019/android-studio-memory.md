---
title:      "android studio 开启AVD提示无法分配内存"
cover:      "https://image.123m.me/images/2019/02/02/1d68f6473df3021187a57f102d403093.png"
date:       "2019-02-25 10:02:07"
tags:
    - 开发工具
---


开启android studio的AVD虚拟时，左下角提示无法分配内存，这种情况一般都是开启了virtualbox的缘故。  
```bash
# 查看是否有使用的进程
ps -ef | grep virtualbox
```  
如果是两者并存的情况下，开通AVD的时候就会提示该错误，将virtualbox关闭即可解决。