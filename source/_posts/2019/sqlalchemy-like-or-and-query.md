---
title:      "SQLAlchemy的模糊查询及and/or查询"
cover:      "https://image.123m.me/images/2019/02/02/a68070659ce0d9f5355bc2c3daf4e62c.md.png"
date:       "2019-03-26 16:57:43"
tags:
    - Python
---

1. 等于查询: `query.filter(User.name == 'leela')`
2. 不等于查询: `query.filter(User.name != 'leela')`
3. 模糊查询: `query.filter(User.name.like('%leela%'))`
4. IN查询: `query.filter(User.name.in_(['leela', 'akshay', 'santanu']))`
5. IN嵌套查询: `query.filter(User.name.in_(session.query(User.name).filter(User.name.like('%santanu%'))))`
6. NOT IN查询: `query.filter(~User.name.in_(['lee', 'sonal', 'akshay']))`
7. IS NULL查询: `query.filter(User.name == None)`
8. IS NOT NULL查询: `query.filter(User.name != None)`
9. AND查询:
```python
from sqlalchemy import and_
query.filter(and_(User.name == 'leela', User.fullname == 'leela dharan'))
# 或者这种
query.filter(User.name == 'leela', User.fullname == 'leela dharan')
# 或者这种
query.filter(User.name == 'leela').filter(User.fullname == 'leela dharan')
```
10. OR查询:
```python
from sqlalchemy import or_
query.filter(or_(User.name == 'leela', User.name == 'akshay'))
```
11. match查询: `query.filter(User.name.match('leela'))`