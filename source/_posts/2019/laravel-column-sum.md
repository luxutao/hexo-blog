---
title:      "Laravel ORM各个字段进行相加的和计算"
cover:      "https://image.123m.me/images/2019/02/02/f64024eddcc0eed3e86bf528fa3c3502.png"
date:       "2019-04-09 10:04:25"
tags:
    - PHP
    - Laravel
---

#### 下面是计算各个字段相加的代码,并且四舍五入
```php
$data = DB::table($table)->first(
    [
    DB::raw('ROUND(SUM(field33+field34), 2) as basic'),
    DB::raw('ROUND(SUM(field39+field41+field42+field43), 2) as subsidy'),
    DB::raw('ROUND(SUM(field36), 2) as unit'),
    DB::raw('ROUND(SUM(field37+field38), 2) as bonus'),
    DB::raw('ROUND(SUM(field48), 2) as compensate'),
    DB::raw('ROUND(SUM(field40+field44+field45+field64), 2) as other'),
    DB::raw('ROUND(SUM(field87), 2) as company'),
    DB::raw('ROUND(SUM(field88), 2) as staffcost'),
    ]
);
```

#### 结果
```json
{
    "basic": 123,
    "subsidy": 123,
    "unit": 123,
    "bonus": 123,
    "compensate": 123,
    "other": 123,
    "company": 123,
    "staffcost": 123
}
```