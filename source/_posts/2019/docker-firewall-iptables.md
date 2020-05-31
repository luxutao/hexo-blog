---
title:      "docker、firewalld、iptables之间的关系"
cover:      "https://image.123m.me/images/2019/02/02/b3d839d6236b55cd884d72717830ef6e.md.png"
date:       "2019-04-26 15:18:18"
tags:
    - Linux
    - Docker
---

docker命令中使用 -p 暴露端口时，实现需要依赖iptables.   
CentOS 7默认使用的是firewalld,这样就会导致两个同时存在.当然如果是继续使用的iptables就没有什么问题了,如果是使用firewall,就需要设置一点东西了.

```bash
sudo firewall-cmd --permanent --zone=trusted --add-interface=docker0
sudo firewall-cmd --permanent --zone=trusted --add-port=8888/tcp
sudo firewall-cmd --reload
```

设置成为这样的就是单独只是使用firewall,而不用iptables了.