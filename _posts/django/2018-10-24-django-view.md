---
title: "[django] 장고 뷰(View)"
layout: post
tag:
- django
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# create view & check

장고에서 뷰를 생성하고 웹에서 확인해보기

## 1. url

URL은 Uniform Resource Locator의 약자로, 웹에서 특정 자원의 위치를 나타낸다. urls.py 파일에 자원들의 위치를 명시해야 장고가 해당 자원을 찾아갈 수 있다.

### blog 앱에 url 추가
```
# vi ./blog/urls.py
# blog 앱에서 접근 가능한 자원들의 위치를 추가시킨다

from django.conf.urls import url
from . import views

urlpatterns = [
        url(r'^$', views.post_list, name='post_list'),
]
```
- url 메소드의 맨 앞에 오는 인자는 정규 표현식으로 표현한 패턴
- 두 번째 오는 인자는 view 메소드 (`2. view` 에서 만들것이다)
- 세 번째 오는 인자는 url의 이름으로, view를 식별한다.

```
1. Group

    (r'^blogs/([0-9])$', views.post_list)

    위의 경우, ()로 둘러쌓인 부분을 Group이라고 한다.
 
    입력된 url이 '/blog/4' 일때

    views.post_list(request, '4') 와 같이 Group의 값을 view 메소드로 넘겨 호출하게 된다.

2. Named Group

    (r'^blogs/(?P<number>[0-9])$', views.post_list) 와 같이 Named Group으로도 정의할 수 있다.

    이 경우에는 views.post_list(request, number='4') 와 같이 view 메소드를 호출한다.
```


### blog urls를 메인 urls에 추가
```python
# vi ./mydjango/urls.py

from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'', include('blog.urls')),
]
```

## 2. view

view는 말그대로 화면에 데이터를 어떻게 보여주느냐 하는 방식을 기술한 메소드로, 화면에 뿌려줄 데이터를 가공하는 역할을 한다.

기본적으로 request를 받아 response를 return하는 구조이며, Django에서는 좀 더 복잡한 처리를 위해 view template을 사용한다.

### blog view 선언
```
# vi ./blog/views.py

def post_list(request):
    return render(request, 'blog/post_list.html', {})
```

- 앞선 url 예제에서 `url(r'^$', views.post_list, name='post_list')` 를 통해 url을 선언하고 있다.
- 이대로 실행하면 views.post_list가 존재하지 않는다고 나오므로, 여기에 들어갈 views.post_list를 만든 것이다.
- 그리고 해당 코드에서도 현재 `blog/post_list.html`이 존재하지 않는다. `3. Template` 에서 만들것이다.


## 3. Template

template은 실제 화면에 보여질 HTML 파일을 의미하며, Django에서는 `./[app]/templates/` 경로를 기본 경로로 template을 인식한다.

### Template 생성


```
mkdir -p ./blog/templates/blog
vi ./blog/templates/blog/post_list.html
```

- template을 찾을때 전체 templates/ 경로 내에서 파일을 찾기 때문에, 두 개의 앱이 동일한 탬플릿명을 사용할 경우 충돌이 날 수 있다 
- 따라서 정확히 앱 이름을 한 번 더 명시하여, 해당 디렉토리 아래에 템플릿을 위치시키는 것이 관리에 용이하다.


### Template에 간단한 문자열 입력 후 웹에서 확인

```html
<!-- vi ./blog/templates/blog/post_list.html -->

<html>
    <head>
        <title>Django Web</title>
    </head>
    <body>
        <h3>Hello, World</h3>
    </body>
</html>
```

## 4. 정리

장고에서는 MTV(Model, Template, View) 패턴을 따르며, 기본적으로 MVC와 많이 유사하다.

- Model : 데이터를 표현, 하나의 모델 클래스는 DB에서 하나의 테이블로 표현됨
- Template : 화면에 보여주기위한 프리젠테이션 로직만을 가짐, View에게 받은 데이터를 템플릿에 동적으로 적용함
    - 일반적인 MVC패턴에서 View와 비슷한 역할
- View : HTTPRequest를 받아 HTTPResponse를 리턴, Model과 Template를 중개함 (비즈니스 로직의 핵심)
    - 일반적인 MVC패턴에서 Controller와 비슷한 역할



화면에 데이터가 보여지는 방식

1. 웹에 특정 url이 입력되면
2. 해당 규칙에 맞는 url에서 view를 불러온다.
3. view에서는 다시 특정 데이터를 가공해서 생성한 html을 불러온다. (view에서 던져준 데이터를 html에서 pythonic하게 조작 가능)
4. html은 templates에 위치해있다.
