---
title:      "Linux下teamviwer一直提示无网络"
cover:      "https://image.animekid.cn/images/2019/02/02/9a12f66e0c43fffbee3e50eaab439740.md.png"
date:       "2019-02-01 14:14:37"
tags:
    - Linux Desktop
---

在Linux Desktop中，teamviewer一直提示`Not ready. Please check your connection`,但是网络却是正常的，这种情况下只需要执行一下teamviewer的守护进程即可：  
```bash
sudo teamviewer daemon stop
sudo teamviewer daemon start
```
