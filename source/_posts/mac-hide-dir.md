---
title:      "Mac下打开finder的隐藏目录"
cover:      "https://image.animekid.cn/images/2019/02/02/3f0c140656a20f12a0bff01aced6972d.md.png"
date:       "2019-02-01 14:14:37"
tags:
    - Mac
---

#### 第一种办法：
```bash
defaults write com.apple.finder AppleShowAllFiles TRUE
killall Finder
```
同理将上面的TRUE改回FALSE就可以恢复隐藏  

#### 第二种办法：
```bash
cd /
sudo chflangs nohidden *
```
要恢复隐藏属性：
```bash
sudo chflags hidden *
```