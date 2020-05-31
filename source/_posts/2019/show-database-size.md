---
title:      "mysql查看数据库或者表的大小"
cover:      "https://image.123m.me/images/2019/02/02/3938bdce3e9d6131b5ef223baf59d98c.md.png"
date:       "2019-03-25 10:52:36"
tags:
    - MYSQL
---

1. 查看该数据库实例下所有库大小，得到的结果是以MB为单位 
```sql
mysql> select table_schema,sum(data_length)/1024/1024 as data_length,sum(index_length)/1024/1024 \
as index_length,sum(data_length+index_length)/1024/1024 as sum from information_schema.tables;
+--------------------+---------------+--------------+---------------+
| table_schema       | data_length   | index_length | sum           |
+--------------------+---------------+--------------+---------------+
| information_schema | 2734.92757511 |  86.27539063 | 2821.20296574 |
+--------------------+---------------+--------------+---------------+
```

2. 查看该实例下各个库大小
```sql
mysql>  select table_schema, sum(data_length+index_length)/1024/1024 as total_mb, \
sum(data_length)/1024/1024 as data_mb, sum(index_length)/1024/1024 as index_mb, \
count(*) as tables, curdate() as today from information_schema.tables group by table_schema order by 2 desc;
+--------------------+---------------+---------------+-------------+--------+------------+
| table_schema       | total_mb      | data_mb       | index_mb    | tables | today      |
+--------------------+---------------+---------------+-------------+--------+------------+
| data_1234567890    | 2820.59610939 | 2734.39689064 | 86.19921875 |     65 | 2015-11-02 |
| mysql              |    0.60579967 |    0.53744030 |  0.06835938 |     14 | 2015-11-02 |
| information_schema |    0.00781250 |    0.00000000 |  0.00781250 |     35 | 2015-11-02 |
+--------------------+---------------+---------------+-------------+--------+------------+
```

3. 查看单个库的大小
```sql
mysql> select concat(truncate(sum(data_length)/1024/1024,2),'mb') as data_size, \
concat(truncate(sum(max_data_length)/1024/1024,2),'mb') as max_data_size, \
concat(truncate(sum(data_free)/1024/1024,2),'mb') as data_free, \
concat(truncate(sum(index_length)/1024/1024,2),'mb') as index_size\
 from information_schema.tables where table_schema = 'erongtu_tyb2014'; 
+-----------+------------------+-----------+------------+
| data_size | max_data_size    | data_free | index_size |
+-----------+------------------+-----------+------------+
| 2734.40mb | 83483426815.99mb | 14.06mb   | 86.19mb    |
+-----------+------------------+-----------+------------+
```

4. 查看单个表的状态
```sql
mysql> show table status from data_1234567890 where name = 'data_1234567890_ss' \G
*************************** 1. row ***************************
           Name: data_1234567890_ss
         Engine: InnoDB
        Version: 10
     Row_format: Compact
           Rows: 840065
 Avg_row_length: 477
    Data_length: 401473536
Max_data_length: 0
   Index_length: 0
      Data_free: 6291456
 Auto_increment: 882251
    Create_time: 2015-09-07 17:24:18
    Update_time: NULL
     Check_time: NULL
      Collation: utf8_general_ci
       Checksum: NULL
 Create_options:
        Comment:
1 row in set (0.00 sec)
```

5. 查看单库下所有表的状态
```sql
mysql> select table_name, (data_length/1024/1024) as data_mb , (index_length/1024/1024) \
as index_mb, ((data_length+index_length)/1024/1024) as all_mb, table_rows \
from tables where table_schema = 'data_1234567890';
+---------------------------+---------------+-------------+---------------+------------+
| table_name                | data_mb       | index_mb    | all_mb        | table_rows |
+---------------------------+---------------+-------------+---------------+------------+
| ss_daccount               |    0.23437500 |  0.10937500 |    0.34375000 |       4481 |
| ss_daccount_log           |    2.48262787 |  0.58496094 |    3.06758881 |      27248 |
| ss_daccount_type          |    0.00025558 |  0.00195313 |    0.00220871 |          8 |
| ss_daccountlog            |  221.61502457 | 22.66113281 |  244.27615738 |    1045462 |
| ss_dactives               |    0.00178146 |  0.00195313 |    0.00373459 |          7 |
+---------------------------+---------------+-------------+---------------+------------+
```