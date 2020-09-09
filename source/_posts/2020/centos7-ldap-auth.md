---
title:      "centos7使用LDAP验证配置"
cover:      "https://image.123m.me/images/2019/02/02/09ce41aa7282eb1fa51b548ab191c7c2.md.png"
date:       "2020-09-09 13:51:16"
tags:
    - Centos
---

centos7使用了ldap进行验证，ssh登录和gnome登录均报错，提示用户uid问题及用户的密码无效  
`pam_unix(gdm-password:auth): auth could not identify password for [xxx]`  
`pam_succeed_if(gdm-password:auth): requirement "uid >= 1000" not met by user `

1. 修改/etc/pam.d/system-auth和/etc/pam.d/password-auth，将里面的uid数字改成其他数字。 
```shell
auth        requisite     pam_succeed_if.so uid >= 500 quiet_success
account     sufficient    pam_succeed_if.so uid < 500 quiet
```
2. 启动服务
```shell
systemctl start sssd
systemctl start oddjobd
```
3. 重启机器