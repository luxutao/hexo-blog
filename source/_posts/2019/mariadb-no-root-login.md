---
title:      "解决Mariadb安装之后无法root登录"
cover:      "https://image.123m.me/images/2019/02/02/b5e68c2b7be749982056f67ab91afbb0.md.png"
date:       "2019-05-10 15:17:16"
tags:
    - Mysql
    - Ubuntu
---

#### 新版本Mariadb安装后无法登录问题的解决

原因是ubuntu安装之后没有启用root用户，所以没有root用户密码，而新安装的mariadb使用的系统root的密码（初始安装后）
通过原来的方法重置password无效（原因就是采用了unix_socket认证）
如果，你希望采用原来的mysql密码方式，需要修改认证插件，方法如下：

```sql
update mysql.user set plugin='mysql_native_password' where user='root';
update mysql.user set password=password("您的密码") where user='root'; 
FLUSH PRIVILEGES;
```
这样就可以在任何用户下访问mysql了。