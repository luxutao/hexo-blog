---
title:      "更改ls命令查看的显示时间格式"
cover:      "https://image.animekid.cn/images/2019/02/02/73474c12d8b341d76b9efee6fc2af1dd.md.png"
date:       "2019-03-08 10:46:39"
tags:
    - Linux
---

1. 系统默认显示时间
```bash
[liul@test dataload]$ ls -l  
total 28896  
drwxr-xr-x 8 liul liul     4096 Sep 24 17:10 PyYAML-3.10  
-rw-r--r-- 1 liul liul   241524 Sep 24 16:40 PyYAML-3.10.tar.gz  
-rwxr-xr-x 1 liul liul 14466821 Feb 16  2012 greenplum-loaders-4.2.1.0-build-2-RHEL5-x86_64.bin  
-rw-r--r-- 1 liul liul 14304561 Mar  1  2012 greenplum-loaders-4.2.1.0-build-2-RHEL5-x86_64.zip  
drwxrwxr-x 5 liul liul     4096 Oct  9 17:53 install  
drwxrwxr-x 2 liul liul     4096 Oct  9 17:58 shell  
drwxr-xr-x 8 liul liul     4096 Oct  9 23:51 yaml-0.1.4  
-rw-r--r-- 1 liul liul   471759 Sep 24 16:47 yaml-0.1.4.tar.gz  
```

2. 修改ls显示格式后效果
```bash
[liul@test dataload]$ ls -l --time-style '+%Y/%m/%d %H:%M:%S'  
total 28896  
drwxr-xr-x 8 liul liul     4096 2012/09/24 17:10:17 PyYAML-3.10  
-rw-r--r-- 1 liul liul   241524 2012/09/24 16:40:10 PyYAML-3.10.tar.gz  
-rwxr-xr-x 1 liul liul 14466821 2012/02/16 00:23:25 greenplum-loaders-4.2.1.0-build-2-RHEL5-x86_64.bin  
-rw-r--r-- 1 liul liul 14304561 2012/03/01 17:14:16 greenplum-loaders-4.2.1.0-build-2-RHEL5-x86_64.zip  
drwxrwxr-x 5 liul liul     4096 2012/10/09 17:53:00 install  
drwxrwxr-x 2 liul liul     4096 2012/10/09 17:58:26 shell  
drwxr-xr-x 8 liul liul     4096 2012/10/09 23:51:18 yaml-0.1.4  
-rw-r--r-- 1 liul liul   471759 2012/09/24 16:47:13 yaml-0.1.4.tar.gz  
```

3. 修改配置到bashrc
```bash
[liul@test dataload]$ vi ~/.bashrc
export TIME_STYLE='+%Y/%m/%d %H:%M:%S'  
[liul@test dataload]$ source ~/.bashrc
```

4. 系统变量生效
```bash
[liul@test dataload]$ ls -l  
total 28896  
drwxr-xr-x 8 liul liul     4096 2012/09/24 17:10:17 PyYAML-3.10  
-rw-r--r-- 1 liul liul   241524 2012/09/24 16:40:10 PyYAML-3.10.tar.gz  
-rwxr-xr-x 1 liul liul 14466821 2012/02/16 00:23:25 greenplum-loaders-4.2.1.0-build-2-RHEL5-x86_64.bin  
-rw-r--r-- 1 liul liul 14304561 2012/03/01 17:14:16 greenplum-loaders-4.2.1.0-build-2-RHEL5-x86_64.zip  
drwxrwxr-x 5 liul liul     4096 2012/10/09 17:53:00 install  
drwxrwxr-x 2 liul liul     4096 2012/10/09 17:58:26 shell  
drwxr-xr-x 8 liul liul     4096 2012/10/09 23:51:18 yaml-0.1.4  
-rw-r--r-- 1 liul liul   471759 2012/09/24 16:47:13 yaml-0.1.4.tar.gz  
[liul@test dataload]$ 
``` 

[源链接](https://blog.csdn.net/qq_26614295/article/details/78899978)