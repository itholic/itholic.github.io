---
title: "[django] 장고 쿼리셋(QuerySet) API"
layout: post
tag:
- django
- python
category: blog
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# Model API

Django에서 Model클래스를 정의하면, 데이터를 삽입/갱신/삭제할 수 있는 다양한 DB API를 제공한다.

## 1. INSERT

INSERT는 save()메소드를 통해 제공한다.

```
class Post(models.Model):
    title = models.CharField(max=100)
    contents = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    
    def publish(self):
        self.save()
```

'publish'에서 save() 메소드를 사용해 객체 자신의 정보를 DB에 INSERT하고있다.

save() 메소드가 실행되면 INSERT SQL문이 생성되고, 바로 테이블에 데이터가 삽입된다.

## 2. SELECT

SELECT는 `클래스.object` 형태로 사용한다.

```python
Post.objects.all()  # SELECT * FROM blog_post;
Post.objects.get(pk=1)  # SELECT * FROM blog_post WHERE pk = 1 LIMIT 1;
Post.objects.filter(pk=1)  # SELECT * FROM blog_post WHERE pk = 1;
Post.objects.exclude(pk=1)  # SELECT * FROM blog_post WHERE pk != 1;
Post.objects.count() # SELECT count(*) FROM blog_post;
Post.objects.order_by(pk, -title) # SELECT * FROM blog_post ORDER BY pk asc, title desc;
Post.objects.distinct(author) # SELECT DISTINCT * FROM blog_post;
Post.objects.first() # SELECT * FROM blog_post WHERE pk = min(pk) LIMIT 1;
Post.objects.last() # SELECT * FROM blog_post WHERE pk = max(pk) LIMIT 1;
```

## 3. UPDATE

UPDATE는 get()을 사용해 로우 객체를 가져와서 변경 후, save()를 이용해 다시 넣는다.

```python
data = Post.objects.get(pk=1)
data.author = 'KDC'
data.save()
```

## 4. DELETE

DELETE는 get()을 사용해 로우 객체를 가져온 후, delete()로 지운다.


```python
data = Post.objects.get(pk=1)
data.delete()
```
