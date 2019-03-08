---
title: "[python] setter, getter (feat. @property)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 프로퍼티

클래스의 속성에 값을 저장하거나 가져올때 대개 다음과 같이 getter/setter메소드를 사용한다.

```python
  1 class PersonClass:
  2     def __init__(self):
  3         self._name = ""
  4
  5     def name_getter(self):
  6         return self._name
  7
  8     def name_setter(self, text):
  9         self._name = text
 10
 11
 12 person1 = PersonClass()
 13 person1.name_setter("lee")
 14 print(person1.name_getter())  # lee
```


5번째 줄에서 `_name` 의 값을 가져오기 위한 `name_getter` 를,

8번째 줄에서 `_name` 에 값을 저장하기 위한 `name_setter` 를 선언했다.

12~14 줄에서 `person1` 이라는 인스턴스를 생성하고, 이름을 지정 후, 리턴 값을 출력했다.

<br/>

위 코드는 `@property` 라는 데코레이터를 통해 다음과 같이 표현할 수 있다.

```python
  1 class PersonClass:
  2     def __init__(self):
  3         self._name = ""
  4
  5     @property
  6     def name(self):
  7         return self._name
  8
  9     @name.setter
 10     def name(self, text):
 11         self._name = text
 12
 13
 14 person1 = PersonClass()
 15 person1.name = "lee"
 16 print(person1.name)
```

getter 함수의 이름을 `name_getter`에서 단순히 `name`으로 바꾸고,

상단에 `@property` 라는 데커레이터를 추가했다.

setter 함수의 이름은 `name_setter`에서 마찬가지로 `name`으로 바꾸고,

상단에 `@name.setter` 라는 데커레이터를 추가했다.

그리고 실제 사용하는 부분에서는 마치 일반 속성처럼 `person1.name` 으로 접근한 것을 볼 수 있다.

코드가 훨씬 직관적으로 변할 것을 확인할 수 있다.
