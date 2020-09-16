---
title:      "更改Django的settings.py"
cover:      "https://image.123m.me/images/2019/02/02/69b3691a0f31338cbac6aa7a0e88feea.png"
date:       "2019-02-01 14:13:13"
tags:
    - Python
    - Django
---

#### 使用mysql数据库
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        # 数据库名称
        'NAME': 'blog',
        # 数据库账号
        'USER': 'root',
        # 数据库密码
        'PASSWORD': '123456',
        'PORT': '3306',
        # 数据库地址
        'HOST': '172.168.1.100',
        'OPTIONS': {
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
            'charset': 'utf8',
        },
    }
}
```

#### 配置自定义验证模块
```python
AUTHENTICATION_BACKENDS = (
    'blockhead.author.UserAuthor',
)
```

#### 更改插入时间时区
```python
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'Asia/Shanghai'    #选择本地区域
USE_I18N = True
USE_L10N = True
USE_TZ = False            #关闭UTC
```
