---
title: "[python] generator 함수"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# generator 함수

generator함수는 얼핏 함수와 비슷하지만, 호출시 generator 객체를 반환한다.

generator 객체는 Iterable하며, next() 메소드를 통해 다음 yield 값을 리턴한다.

리턴할 yield 값이 떨어지면 StopIteration 예외를 발생시킨다.

말로만 하면 이해가 안되니 코드를 보자.

```python
  1 # -*- coding:utf-8 -*-
  2
  3
  4 def generator():
  5     yield 10
  6
  7
  8 gen = generator() 
  9 print(gen)  # <generator object generator at 0x10b2f5aa0>
 10 next(gen)  # 10
 11 next(gen)  # StopIteration
```

(4~5) 10을 yield하는 generator 함수를 선언했다.

(8) 일반 함수였다면 gen에 숫자 10이 return되었을 것이다.

(9) 하지만 gen을 출력해보면 generator object가 할당된 것을 확인할 수 있다.

(10) next() 함수를 써서 generator를 호출하면, 그제서야 값이 yield되어 10이라는 값이 튀어나온다. 

(11) 한 번 더 generator를 호출하려고하면, 값이 모두 바닥났으므로 StopIteration 에러가 발생한다.

<br/>

이번엔 여러 개의 값을 yield 하는 generator 함수를 만들어보자.

```python
def generator_many(cnt):
    while cnt != 0:
        yield cnt
        cnt -= 1


gen = generator_many(5)
next(gen)  # 5
next(gen)  # 4
next(gen)  # 3
next(gen)  # 2
next(gen)  # 1
next(gen)  # StopIteration
``` 

만약 generator\_many가 generator 함수가 아닌 일반 함수였다면 (yield 대신 return 했다면)

단순히 숫자 5를 한 번 반환하고 종료되었을 것이다.

하지만 제네레이터 함수는 next를 호출할 때마다 생성해 낼 수 있는 값이 바닥날때까지 값을 반환해준다.

<br/>

generator 함수로 값을 넘겨주는 것 또한 가능하다. 

send 메소드를 통해 yield를 받는 변수에 값을 넘기고, next()가 자동으로 실행된다.

```python
>>> def generator_send():
...     while True:
...         receive = yield 10
...         print receive
...
>>>
>>> gen = generator_send()
>>>
>>>
>>> next(gen)
10
>>>
>>> next(gen)
None
10
>>>
>>> next(gen)
None
10
>>>
>>> gen.send('hi')
hi
10
>>>
>>> gen.send('hello !!')
hello !!
10
>>>
```

generator를 종료하고싶다면 `close(gen)`을 통해 종료 가능하다 (GeneratorExit 예외를 반환한다)

참고로 이런식으로 함수가 한 번 호출후 바로 사라지지 않고 계속 살아있으면서,

메인루틴과 지속적인 협력관계를 유지하는 루틴을 coroutine이라고 한다.

## 20190210: Youtube 설명 보충

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZYnyiYSHvXQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
