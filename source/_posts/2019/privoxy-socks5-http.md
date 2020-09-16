---
title:      "使用privoxy将socks5代理转换为http"
cover:      "https://image.123m.me/images/2019/02/02/e32df8547dcb43b5a2df04d05121bc8e.jpg"
date:       "2019-02-25 09:56:29"
tags:
    - Linux Desktop
---

1. 安装privoxy  
```bash
sudo apt install privoxy
```

2. 更改配置文件  
```bash
sudo vi /etc/privoxy/config
# 找到socks5 的行数，将注释去掉更改为
forward-socks5  /   127.0.0.1:1080  .
# 1080 为socks的默认端口，如果更改过请修正为更改后的端口
#另外监听接口默认开启的 127.0.0.1:8118 如果有需要可以配置，没有需要就不用。  
```

3. 开启服务  
```bash
sudo systemctl start privoxy
```