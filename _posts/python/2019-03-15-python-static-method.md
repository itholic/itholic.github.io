---
title: "[python] @staticmethod"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 스태틱 메서드

<a href="" target="_blank">이전 포스팅</a>에서 클래스 메서드(@classmethod)에 대해 알아봤다.

클래스 메서드를 공부하다보면 스태틱 메서드(@staticmethod)라는 녀석이 종종 따라온다.

그래서 이번에는 스태틱메서드가 무엇인지 알아보려고한다.

<br/>

이전 포스팅에서 사용했던 예제를 살짝 변경해보자.

```python
  1 class MyClass:
  2     @classmethod
  3     def my_doubler_class(cls, num):
  4         print(num * 2)
  5
  6     @staticmethod
  7     def my_doubler_static(num):
  8         print(num * 2)
```

MyClass라는 클래스를 만들고, `my_doubler_class`, `my_doubler_static` 두 개의 함수를 정의했다.

두 함수 모두 전달받은 숫자에 2를 곱한 결과를 출력해주는 기능을 한다.

`my_doubler_class` 함수 위에는 `@classmethod` 라는 데커레이터를,

`my_doubler_static` 함수 위에는 `@staticmethod` 라는 데커레이터를 붙여 함수를 정의했다.

<br/>

우선 일반적인 방식으로 클래스를 인스턴스화 하고, 함수를 사용해보자.

```python
  1 class MyClass:
  2     @classmethod
  3     def my_doubler_class(cls, num):
  4         print(num * 2)
  5
  6     @staticmethod
  7     def my_doubler_static(num):
  8         print(num * 2)
  9
 10
 11 mc = MyClass()
 12 mc.my_doubler_class(10)  # 20
 13 mc.my_doubler_static(10)  # 20
```

(11) mc라는 변수로 MyClass 인스턴스를 생성하고,

(12~13) `my_doubler_class` 와 `my_doubler_static` 에 10을 넣어 실행해보자.

두 경우 모두 '20' 이라는 결과를 똑같이 반환한다.

<br/>

또한, 클래스 메서드와 스태틱 메서드는 둘 다 인스턴스화 하지 않고 호출 가능하다.

```python
  1 class MyClass:
  2     @classmethod
  3     def my_doubler_class(cls, num):
  4         print(num * 2)
  5
  6     @staticmethod
  7     def my_doubler_static(num):
  8         print(num * 2)
  9
 10
 11 MyClass.my_doubler_class(10)  # 20
 12 MyClass.my_doubler_static(10)  # 20
```

하지만 만약 클래스 내에서 사용하는 변수를 참조해야 한다면,

스태틱 메서드의 경우는 참조가 불가능하다.

```python
  1 class MyClass:
  2     print_format = "{} * 2 = {}"
  3     @classmethod
  4     def my_doubler_class(cls, num):
  5         print(cls.print_format.format(num, num * 2))
  6
  7     @staticmethod
  8     def my_doubler_static(num):
  9         print(print_format.format(num, num * 2))
 10
 11
 12 MyClass.my_doubler_class(10)  # 20
 13 MyClass.my_doubler_static(10)  # NameError: name 'print_format' is not defined
```

(13) 스태틱 메서드의 경우 클래스 내부에서 정의된 `print_format` 을 참조하지 못하는 것을 볼 수 있다.

self를 통한 접근도 당연히 안된다.

<br/>

즉, 스태틱 메서드는 그냥 클래스 바깥에 정의된 일반 함수와 완전히 동일하게 동작한다.

다만, 특정 클래스와 보다 밀접한 관계가 있다는 것을 나타내기위해,

혹은 조금이라도 코드를 줄여 간단하게 표현하기 위해 @staticmethod 키워드를 사용해 정의하는 것으로 보인다.

@staticmethod를 쓰거나 쓰지 않는다고 해서 성능 및 기능적으로 크리티컬하게 문제될건 없어보이니,

개인의 취향에 맞게 선택하면 될 것 같다.
