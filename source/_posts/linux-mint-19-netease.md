---
title:      "解决Linux mint19.1 无法打开网易云音乐"
cover:      "https://image.animekid.cn/images/2019/02/02/8edee17ea3ee666709cbeebb9267c4ab.md.png"
date:       "2019-02-01 14:14:37"
tags:       
    - Linux Desktop
---

#### 安装完成Linux mint19.1之后无法双击打开网易云音乐

##### 安装网易云音乐：
`sudo dpkg -i 文件路径`
##### 文件路径可以直接把刚才下载的软件包拖进终端：
`sudo apt install -f` 修复依赖关系


#### 安装后打不开的问题：

#### 第一种解决
1. 如果root用户没有密码需要先给root用户设置密码：  
`sudo passwd root`
2. 编辑sudo权限文件：  
`sudo vi /etc/sudoers` 在最后面加一行：  
`lzz ALL = NOPASSWD: /usr/bin/netease-cloud-music`  
**注：lzz为当前登录用户名**
3. 编辑双击打开的桌面文件：  
`sudo vi /usr/share/applications/netease-cloud-music.desktop`  
修改`Exec=netease-cloud-music %U`为 `Exec=sudo netease-cloud-music %U`  
这样点击网易云音乐图标就可以启动的了。  

#### 第二种解决
编辑双击打开的桌面文件：
`sudo vi /usr/share/applications/netease-cloud-music.desktop`  
修改`Exec=netease-cloud-music %U`为 `sh -c "unset SESSION_MANAGER &&  netease-cloud-music %U"`  
这样点击网易云音乐图标就可以启动的了。


#### 如果无法保存配置，请执行下列命令  
可能的原因是使用sudu启动过，所以权限变成了root，导致没有权限
```bash
cd ~/.config
sudo chown -R username:username netease-cloud-music/
cd ~/.cache
sudo chown -R username:username netease-cloud-music/
```