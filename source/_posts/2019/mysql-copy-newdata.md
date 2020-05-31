---
title:      "MySQL使用命令行复制表结构和数据"
cover:      "https://image.123m.me/images/2019/02/02/ac3e2a92ab5c12aa7f0a241c4ad6c639.md.png"
date:       "2019-04-09 10:10:54"
tags:
    - MySQL
---

#### mysql中用命令行复制表结构的方法主要有一下几种: 

1. 只复制表结构到新表  
`CREATE TABLE 新表 SELECT * FROM 旧表 WHERE 1=2;`  
或  
`CREATE TABLE 新表 LIKE 旧表;`  
注意上面两种方式，前一种方式是不会复制时的主键类型和自增方式是不会复制过去的，而后一种方式是把旧表的所有字段类型都复制到新表。

2. 复制表结构及数据到新表  
`CREATE TABLE 新表 SELECT * FROM 旧表;`
 
3. 复制旧表的数据到新表(假设两个表结构一样)  
`INSERT INTO 新表 SELECT * FROM 旧表;`
 
4. 复制旧表的数据到新表(假设两个表结构不一样)
`INSERT INTO 新表(字段1,字段2,.......) SELECT 字段1,字段2,...... FROM 旧表;`