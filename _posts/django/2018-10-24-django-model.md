---
title: "[django] 장고 모델(Model)"
layout: post
tag:
- django
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# create model & check

장고에서 모델을 생성하고 웹에서 확인해보기


## 1. 앱

장고에서 앱이란, 비슷한 유형의 특정 기능들을 수행하는 페이지들의 모임라고 이해하면 쉽다. 예를들면 각종 정보를 포스팅하는 'BLOG'라는 앱이 있을 수 있고, 회원 정보를 관리하는 'USERS'라는 앱이 있을 수 있다.


### blog 앱 생성
```
python manage.py startapp blog
```
- 앱이 생성되면 다음과 같이 디렉토리가 구성된다.

```
./
|---manage.py
|---mydjango
    |---settings.py
    |---urls.py
    |---wsgi.py
    |---__init__.py
    |---blog
        |---__init__.py
        |---admin.py
        |---models.py
        |---tests.py
        |---views.py
        |---migrations
            |---__init__.py
```

### 장고에 등록
```
vi ./mydjango/settings
INSTALLED_APPS 리스트에 'blog' 추가
```

## 2. 모델

앱 안에서 다시 세부적으로 기능이 나뉘어져서 각 기능을 수행하는 객체를 모델이라고 한다.

### 모델 생성
```python
# vi ./blog/models.py
# models.Model을 상속받아 'Post'라는 모델(Class) 생성    

class Post(models.Model):
    title = models.CharField(max=100)
    contents = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    
    def publish(self):
        self.save()
    
```
models.CharField(max=100) : 고정길이 텍스트
models.TextField() : 가변길이 텍스트
models.DateTimeField(default=timezone.now) : 날짜 및 시간


### blog를 위한 migration파일 생성 및 DB에 반영

모델을 생성하거나 변경하면 해당 내용을 DB에 반영해야하는데, 이를 migration이라 한다.

migration은 migration 파일을 만드는 과정, 파일을 DB에 실제 적용하는 과정으로 나뉜다.

```
python manage.py makemigrations blog
python manage.py migrate blog
```

### blog admin에 'Post' 모델 등록
```python
# vi ./blog/admin.py

from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

### 웹에서 확인
```
127.0.0.1:8000/admin
로그인하면 생성되어있는 'blog'와 'Post'를 볼 수 있음
'POST 추가'에서 앞서 선언한 변수들이 각 필드로 자동 생성된 것을 확인할 수 있음
```
- 로그인시 superuser는 다음 명령으로 생성 가능
```
python manage.py createsuperuser
```


