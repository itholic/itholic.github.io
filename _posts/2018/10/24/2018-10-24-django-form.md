---
titile: "[django] 장고 폼(Form)"
layout: post
tag:
- django
- python
category: blog
author: itholic
sitemap:
  changefreq: weekly
  priority: 1.0
---

# form

Model 객체를 가져다가 좀 더 쉽게 화면을 구성할 수 있게 도와주는 녀석(?) 

일단 만들어보자...


## 1. form 정의

다음과 같은 Model을 기반으로 Form을 만들어보자

```python
# ./blog/models.py

class Post(models.Model):
    title = models.CharField(max=100)
    contents = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    
    def publish(self):
        self.save()
```

앱 디렉토리 밑에 forms.py를 만들어서 작성

```python
# ./blog/forms.py

from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'contents']  # Model 클래스의 필드중, 일부만 사용하고자 할 때
```

폼 작성이 끝났다(?)

이렇게 작성한 폼은 view와 template에서 사용하면 된다.

```python
# ./blog/views.py

def addpost(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid()
            form.save()
        return redirect('post_list')
    else:
        form = PostForm()

    return render(request, 'blog/post_add.html', {'form': form})
```

POST요청이 왔을 경우, POST body의 정합성을 확인해 폼을 저장한다

render를 보면 form이라는 이름으로 빈 form을 post_add.html에게 전달하고 있다.

이는 template에서 다음과 같이 받는다.


```html
<!-- ./blog/templates/blog/post_add.html -->

    <div>
        <form method="POST">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit">save</button>
        </form>
   </div>
```

form.as_p 는 폼을 p태그 안에 배치한다는 의미이다.

비슷한 함수로 form.as_table, form.as_ul 등이 있다.

이는 필드를 Wrapping할 HTML 태그를 지정해주는 것이다.

그리고 {% csrf_token %} 을 통해 Cross Site Request Forgeries 공격에 대해 방지해준다.

이는 POST, PUT, DELETE 메소드 사용시 필수로 넣어주어야한다.


