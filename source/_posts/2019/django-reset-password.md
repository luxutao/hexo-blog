---
title:      "Django重置admin管理密码"
cover:      "https://image.animekid.cn/images/2019/02/02/5896e6a5f36cab8353103355c88fdcf9.md.jpg"
date:       "2019-02-21 16:28:19"
tags:
    - Python
    - Django
---

如果你忘记了设置Django的Admin密码，那么你可以使用createsuperuser来设置密码，但是如果你忘记了Admin的密码的话，那么就要用Django shell：

```shell
python manage.py shell
```

然后获取你的用户名，并且重置密码：

```python
from django.contrib.auth.models import User 
user = User.objects.get(username='admin') 
user.set_password('new_password') 
user.save()
```