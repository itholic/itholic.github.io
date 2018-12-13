---
title: "[python] 파이썬에서 여러 부모의 init 실행하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 여러 부모의 init 실행

다음과 같은 코드가 있다.

```python
  1 class Mother:
  2     def __init__(self):
  3         print('mother')
  4
  5 class Father:
  6     def __init__(self):
  7         print('father')
  8
  9 class Gentleman(Mother, Father):
 10     def __init__(self):
 11         print('gentleman')
 12
 13
 14 Gentleman()
```

9번째 줄의 Gentleman이라는 클래스가 Mother, Father 클래스를 상속받고있다.

14번 라인에서 Gentleman 인스턴스를 생성한 결과는 다음과 같다.

```
gentleman
```

두 개의 부모에게 상속받았지만, 본인의 생성자만 실행하고있다.

상속받은 부모의 생성자를 실행하기 위해서는 기본적으로 다음과 같이 하면 된다.

```python
  1 class Mother:
  2     def __init__(self):
  3         print('mother')
  4
  5 class Father:
  6     def __init__(self):
  7         print('father')
  8
  9 class Gentleman(Mother, Father):
 10     def __init__(self):
 11         super().__init__()
 12         print('gentleman')
 13
 14
 15 Gentleman()
```

11번째 줄에 super() 메소드를 사용해 부모의 생성자를 실행하고있다.

실행 결과를 확인해보자.

```
mother
gentleman
```

두 명의 부모에게 상속받았지만, Mother의 생성자만 실행하고있다.

super() 메소드를 사용한 부모클래스 호출은 클래스 첫 번째 인자로 상속받은 부모를 가리킨다는것을 알 수 있다.

그럼 Father의 생성자는 실행할 수 없을까?

다음과같이 해주면 된다.

```python
  1 class Mother:
  2     def __init__(self):
  3         print('mother')
  4
  5 class Father:
  6     def __init__(self):
  7         print('father')
  8
  9 class Gentleman(Mother, Father):
 10     def __init__(self):
 11         super().__init__()
 12         Father.__init__(self)
 13         print('gentleman')
 14
 15
 16 Gentleman()
```

12번째 줄에 부모의 클래스명과 생성자 메서드를 실행해 부모의 생성자를 실행하고있다.

super()를 통한 초기화와 다른점은 인자로 self를 넘겨준다는 것이다.

실행해보자.

```
mother
father
gentleman
```

모든 부모의 생성자를 실행하며 Gentleman 인스턴스를 생성했다.

참고로 첫 번째 부모의 메소드를 사용하기위해 super() 키워드를 사용할 필요는 없다.

다음과 같이 실행해도 동일한 결과를 얻을 수 있다.

```python

  1 class Mother:
  2     def __init__(self):
  3         print('mother')
  4
  5 class Father:
  6     def __init__(self):
  7         print('father')
  8
  9 class Gentleman(Mother, Father):
 10     def __init__(self):
 11         Mother.__init__(self)
 12         Father.__init__(self)
 13         print('gentleman')
 14
 15
 16 Gentleman()
```

11번째 줄에서 super()로 실행하던 Mother 클래스의 생성자 호출 방식을 변경했다.

결과는 똑같이 나온다.

```
mother
father
gentleman
```
