---
title: "[python] closure"
layout: post
tag:
- python
category: blog
author: itholic
sitemap:
  changefreq: weekly
  priority: 1.0
---

# closure

파이썬은 함수 내부에 함수를 선언할 수 있다.

이는 파이썬에서 함수를 1급 객체로 취급하기 때문이다.

함수에서 내부 함수를 리턴하면, 리턴된 내부 함수는 여전히 외부함수의 변수 값을 사용 가능하다.

이는 closure라는 기능이 있기때문에 가능한 것이다.

코드로 알아보자.

```python
# -*- coding:utf-8 -*-

def outer_func(name, age):
    name = name
    age = age

    def inner_func():
        print("my name is {}, and i am {} years old".format(name, age))

    return inner_func  # 함수 자체를 반환한다

of = outer_func("sowut", "29")  # outer_func는 inner_func를 반환하고 종료됨
of()  # my name is sowut, amd i am 29 years old

# outer_func가 종료되었음에도 불구하고, 여전히 outer_func의 변수인 name과 age를 참조한다
# 이는 클로저가 inner_func의 프리변수인 name과 age를 어딘가에 저장해놓기 때문에 가능하다
# 그 '어딘가'는 바로 이곳이다.
print(of.__closure__[0].cell_contents)  # 29
print(of.__closure__[1].cell_contents)  # sowut

# 다음과 같이 응용 가능하다
def tag_maker(tag):
    tag = tag

    def contents_inserter(contents):
        contents = contents
        print("<{0}>{1}</{0}>".format(tag, contents))

    return contents_inserter

head_contents_inserter = tag_maker("head")  # contents_inserter 리턴
body_contents_inserter = tag_maker("body")  # contents_inserter 리턴

head_contents_inserter("i am head")  # <head>i am head</head>
body_contents_inserter("i am body")  # <body>i am body</body>
```
