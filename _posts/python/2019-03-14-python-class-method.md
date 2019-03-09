---
title: "[python] @classmethod"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 클래스 메서드

가끔 코드를 보다가 클래스 내에서 `@classmethod` 라는 데커레이터를 사용하는 것을 보았다.

클래스에서 사용하는 일반 함수와 무슨 차이가 있을까?

```python
  1 class MyClass:
  2     def my_doubler(self, num):
  3         print(num * 2)
  4
  5     @classmethod
  6     def my_doubler_class_method(cls, num):
  7         print(num * 2)
```

MyClass라는 클래스를 만들고, `my_doubler`, `my_doubler_class_method` 두 개의 함수를 정의했다.

두 함수 모두 전달받은 숫자에 2를 곱한 결과를 출력해주는 기능을 한다.

단, `my_doubler_class_method` 함수 위에는 `@classmethod` 라는 데커레이터를 붙여 클래스 메서드로 정의했다.

<br/>

우선 일반적인 방식으로 클래스를 인스턴스화 하고, 함수를 사용해보자.

```python
  1 class MyClass:
  2     def my_doubler(self, num):
  3         print(num * 2)
  4
  5     @classmethod
  6     def my_doubler_class_method(cls, num):
  7         print(num * 2)
  8
  9
 10 mc = MyClass()
 11 mc.my_doubler(10)  # 20
 12 mc.my_doubler_class_method(10)  # 20
```

(10) mc라는 변수로 MyClass 인스턴스를 생성하고,

(11~12) `my_doubler` 와 `my_doubler_class_method` 에 10을 넣어 실행해보자.

두 경우 모두 '20' 이라는 결과를 똑같이 반환한다.

<br/>

그렇다면 클래스 메서드와 일반 메서드의 차이는 무엇일까?

클래스 메서드는 다음과 같이 인스턴스화 하지 않고 바로 호출 가능하다.


```python
  1 class MyClass:
  2     def my_doubler(self, num):
  3         print(num * 2)
  4
  5     @classmethod
  6     def my_doubler_class_method(cls, num):
  7         print(num * 2)
  8
  9
 10 MyClass.my_doubler_class_method(10)  # 20
```

그럼 `my_doubler` 는 인스턴스화 하지 않고 호출이 불가능할까?

불가능하진 않지만, 다음과 같이 'self' 자리에 들어갈 값을 임의로 넣어주어야한다.

```python
  1 class MyClass:
  2     def my_doubler(self, num):
  3         print(num * 2)
  4
  5     @classmethod
  6     def my_doubler_class_method(cls, num):
  7         print(num * 2)
  8
  9
 10 MyClass.my_doubler(None, 10)  # 20
```

(11) 클래스 메서드인 `my_doubler_class_method`의 경우 cls에 들어가는 값을 생략할 수 있었지만,

일반 메서드인 `my_doubler`의 경우는 self에 들어가는 값을 생략할 수 없어서 `None` 이라는 임의의 값을 넣었다.

이 경우는 클래스 내의 다른 변수에 접근할 일이 없었기때문에 문제 없이 실행이 됐지만,

클래스 내의 특정 변수를 참고해야하는 경우에는 문제가 생긴다.

클래스에 변수를 추가해보자.

```python
  1 class MyClass:
  2     print_format = "{} * 2 = {}"
  3     def my_doubler(self, num):
  4         print(self.print_format.format(num, num * 2))
  5
  6     @classmethod
  7     def my_doubler_class_method(cls, num):
  8         print(cls.print_format.format(num, num * 2))
```

이번엔 그냥 출력하는 것이 아니라 `print_format` 변수에 정해놓은 모양에 맞추어 결과를 출력해준다.

예를들어 `my_doubler(10)` 은 `'10 * 2 = 20'` 이라는 문자열을 출력한다. 

<br/>

앞선 예제와 마찬가지로,

우선 일반적인 방식으로 클래스를 인스턴스화 하고, 함수를 사용해보자.

```python
  1 class MyClass:
  2     print_format = "{} * 2 = {}"
  3     def my_doubler(self, num):
  4         print(self.print_format.format(num, num * 2))
  5
  6     @classmethod
  7     def my_doubler_class_method(cls, num):
  8         print(cls.print_format.format(num, num * 2))
  9
 10
 11 mc = MyClass()
 12 mc.my_doubler(10)  # 10 * 2 = 20
 13 mc.my_doubler_class_method(10)  # 10 * 2 = 20
```

(11) mc라는 변수로 MyClass 인스턴스를 생성하고,

(12~13) `my_doubler` 와 `my_doubler_class_method` 에 10을 넣어 실행해보자.

두 경우 모두 '10 * 2 = 20' 이라는 결과를 똑같이 반환한다.

<br/>

이번에는 인스턴스화 하지 않은 상태로 바로 클래스 메서드를 사용해보자.

```python
  1 class MyClass:
  2     print_format = "{} * 2 = {}"
  3     def my_doubler(self, num):
  4         print(self.print_format.format(num, num * 2))
  5
  6     @classmethod
  7     def my_doubler_class_method(cls, num):
  8         print(cls.print_format.format(num, num * 2))
  9
 10
 11 MyClass.my_doubler_class_method(10)  # 10 * 2 = 20
```

제대로 실행이 되었다.

즉, 클래스에 있는 `print_format` 변수를 가져다가 쓰는데 전혀 문제가 없다.

이번에는 일반 메서드인 `my_doubler`를 인스턴스화 하지 않고 사용해보자.

```python
  1 class MyClass:
  2     print_format = "{} * 2 = {}"
  3     def my_doubler(self, num):
  4         print(self.print_format.format(num, num * 2))
  5
  6     @classmethod
  7     def my_doubler_class_method(cls, num):
  8         print(cls.print_format.format(num, num * 2))
  9
 10
 11 MyClass.my_doubler(None, 10)  # AttributeError: 'NoneType' object has no attribute 'print_format'
```

11번째 줄의 주석을 보자.

해당 스크립트를 실행한 결과 발생한 에러이다.

일반 메서드인 `my_doubler` 는 클래스메서드인 `my_doubler_class_method`와 달리 `print_format` 변수를 참조할 수 없다.

즉, 특정 메서드에 `@classmethod` 데커레이터를 붙여 클래스 메서드로 정의하게되면,

클래스를 인스턴스화 하지 않은 채 클래스 내부의 변수나 함수에 접근해 사용 가능하다.
