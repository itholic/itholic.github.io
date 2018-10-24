---
title: "[django] 장고 디자인패턴(MTV)"
layout: post
tag:
- django
- python
- MTV
- design_pattern
category: blog
author: itholic
sitemap:
  changefreq: weekly
  priority: 1.0
---

# MTV

장고의 개발 방식은 MTV(Model, Template, View) 패턴을 따르며, 기본적으로 MVC와 많이 유사하다.


## Model

Class로 구현되며 데이터를 표현한다. 

하나의 모델 클래스는 DB에서 하나의 테이블로 표현된다.

```python
class Post(models.Model):
    title = models.CharField(max=100)
    contents = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    
    def publish(self):
        self.save() 
```

위 모델에서 title, contents, create_date는 테이블의 필드가 된다.

각 필드는 models.CharField(), models.TextField()등 각 타입에 해당하는 클래스 객체를 생성해 할당한다. 

즉, 필드는 인스턴스 변수가 아닌 클래스 변수로 생성한다.


## Template

HTML로 구현되며 화면에 보여주기위한 프리젠테이션 로직만을 가진다. 

View에게 받은 데이터를 템플릿에 동적으로 적용한다.

일반적인 MVC패턴에서 View와 비슷한 역할


### Django Template Language

Django Template에서 사용하는 문법을 Django Template Language라 한다.

Template 변수, Template 태그, Template 필터, Template 코멘트 등으로 나뉜다.

view에서 이름을 지정해 넘겨준 데이터를 다음과 같이 사용 가능하다.

![탬플릿태그](/assets/images/2018/10/24/django_template_language.png)



## View

메소드로 구현되며, HTTPRequest를 받아 HTTPResponse를 리턴하는 형태이다. 

Model과 View를 중개하며, 비즈니스 로직의 핵심이다.(Model에서 받아온 데이터를 View로 전달)

일반적인 MVC패턴에서 Controller와 비슷한 역할



