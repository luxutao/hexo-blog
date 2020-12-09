---
title:      "Windows命令行用户管理"
cover:      "https://image.123m.me/images/2019/02/02/e87976d31f4836e4ef3b20d6ee3e4f21.md.png"
date:       "2020-12-09 16:24:32"
tags:
    - Windows
    - NetUser
---

1. 创建windows用户，并且第一次登录需要更改密码。 
```cmd
net user {username} {password} /add /logonpasswordchg:yes
```
2. 打开windows用户的网络接入权限，允许访问，适用于vpn。
```cmd
netsh rsa set user {username} permit
```
3. 创建windows域用户，并且第一次登录需要更改密码。 
```cmd
'dsadd user "cn={username},ou=test,ou=test,dc=test,dc=com" '
    '-upn {username}@test.com -mustchpwd yes -samid {username} -pwd {password} '
    '-display {username} -disabled no'
```
4. 修改windows域用户的密码。  
```cmd
'dsmod user "cn={username},ou=test,ou=test,dc=test,dc=com" '
    '-pwd {password} -mustchpwd yes'
```
5. 删除windows域用户。  
```cmd
'dsrm "cn={username},ou=test,ou=test,dc=test,dc=com" -noprompt'
```
6. 添加对应的windows域用户exchange邮箱。  
```cmd
'winpop add {username}@test.com'
```