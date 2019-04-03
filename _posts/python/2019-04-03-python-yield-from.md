---
title: "[python] yield from"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 yield from 간단히 알아보기

파이썬 3.3부터 `yield from` 이라는 키워드를 지원한다.

<br/>

문장 그대로 해석하자면,

yield를 하긴 하는데, 내가 가진 값을 바로 yield 하는게 아니라,

'어딘가'로부터(from) 받아온 값을 yield 해준다는 의미이다.

그 '어딘가'는 바로 iterable한 또다른 객체이다.

전혀 이해가 되지 않을테니, 예제를 통해 어떤 개념인지 간단히 알아보자.

<br/>

다음 코드를 보자.

digit\_gen은 호출할때마다 0과 1을 반복해서 무한 생성해내는 <a href="https://itholic.github.io/python-generator/" target="_blank">제네레이터 함수</a>이다.

```python
  1 from itertools import cycle
  2
  3
  4 def digit_gen():
  5     for digit in cycle(range(2)):
  6         yield digit
  7
  8
  9 one_zero = digit_gen()
 10 next(one_zero)  # 0
 11 next(one_zero)  # 1
 12 next(one_zero)  # 0
 13 next(one_zero)  # 1
 14 next(one_zero)  # 0
 15 next(one_zero)  # 1
 16 next(one_zero)  # 0
```

참고로 itertools의 cycle은,

iterable한 객체를 인자로 전달했을때, 해당 객체를 무한히 반복해주는 iterator를 반환해준다.

딕셔너리를 전달해주면 next()로 호출시 딕셔너리의 key를 반복해서 뱉어낸다.

(for loop에 iterable한 객체를 넣었을때 동작하는 방식을 생각하면 된다)

<br/>

어쨋든 해당 예제에서는 cycle에 range(2)를 주고 for loop을 돌렸기때문에,

next로 호출시 0과 1을 무한히 생성(yield)해내는 것이다.

헷갈리면 range(2) 대신 [0, 1] 이라고 생각하면 된다.

<br/>

위 코드에 yield from 키워드를 적용하면 다음과 같이 나타낼 수 있다.

```python
  1 from itertools import cycle
  2
  3
  4 def digit_gen():
  5     yield from cycle(range(2))
  6
  7
  8 one_zero = digit_gen()
  9 next(one_zero)  # 0
 10 next(one_zero)  # 1
 11 next(one_zero)  # 0
 12 next(one_zero)  # 1
 13 next(one_zero)  # 0
 14 next(one_zero)  # 1
 15 next(one_zero)  # 0
```

5번 라인에서 for loop을 돌리던 부분을 yield from 키워드로 대체하였다.

기존에 cycle객체에 대하여 for loop을 돌며 데이터를 하나씩 yield하던 부분이 사라졌다.

즉, yield 작업에 대한 부분을 cycle에게 위임하였다고 볼 수 있다.

<br/>

이해를 돕기위해 조금 더 예시를 들어보자.

iterable한 객체의 요소를 무한히 생성해내는 제네레이터 함수를 cycle을 사용하지 않고 직접 구현해보자.

이름은 임의로 cycle\_gen으로 해보자.

```python
  1 def cycle_gen(iterable):
  2     while True:
  3         for item in iterable:
  4             yield item
  5
  6
  7 def digit_gen():
  8     for digit in cycle_gen(range(2)):
  9         yield digit
 10
 11
 12 one_zero = digit_gen()
 13 next(one_zero)  # 0
 14 next(one_zero)  # 1
 15 next(one_zero)  # 0
 16 next(one_zero)  # 1
 17 next(one_zero)  # 0
 18 next(one_zero)  # 1
 19 next(one_zero)  # 0
```

(1~4) iterable한 객체를 받아서 for loop을 돌며 요소를 하나씩 반환하는데,

이를 while문에 넣어 요소가 바닥나면 다시 처음부터 반환하게하는 제네레이터 함수를 선언했다.

즉, cycle하고 똑같이 동작하는 제네레이터 함수를 선언했다.

(7~9) 이제 제네레이터 함수인 digit\_gen은 또다른 제네레이터 함수인 cycle\_gen으로부터 값을 생성해내고,

for loop을 돌며 cycle\_gen이 생성(4번 라인의 yield)해준 값을 그대로 다시 생성(9번 라인의 yield)해준다.

<br/>

마찬가지로, 이 코드에 yield from을 적용하면 다음과 같다.

```python
  1 def cycle_gen(iterable):
  2     while True:
  3         for item in iterable:
  4             yield item
  5
  6
  7 def digit_gen():
  8     yield from cycle_gen(range(2))
  9
 10
 11 one_zero = digit_gen()
 12 next(one_zero)  # 0
 13 next(one_zero)  # 1
 14 next(one_zero)  # 0
 15 next(one_zero)  # 1
 16 next(one_zero)  # 0
 17 next(one_zero)  # 1
 18 next(one_zero)  # 0
```

사실 첫 번째 예제와 완전히 동일한 예제이지만, 아마 조금 더 직관적으로 다가올 것이다.

yield from으로 생성을 위임한 제네레이터 함수(cycle\_gen)가 실제 어떻게 구현되어있는지 눈에 보이기 때문이다.

근데, 자세히 보니까 왠지 3~4번 라인에서도 yield from을 사용할 수 있을것 같다.

iterable한 객체(iterable)에서 요소(item)를 받아와 생성(yield)해내고 있지 않은가?

그럼 바꿔보자.

```python
  1 def cycle_gen(iterable):
  2     while True:
  3         yield from iterable
  4
  5
  6 def digit_gen():
  7     yield from cycle_gen(range(2))
  8
  9
 10 one_zero = digit_gen()
 11 print( next(one_zero))  # 0
 12 print( next(one_zero))  # 1
 13 print( next(one_zero))  # 0
 14 print( next(one_zero))  # 1
 15 print( next(one_zero))  # 0
 16 print( next(one_zero))  # 1
 17 print( next(one_zero))  # 0
```

이 코드 또한 다른 에제들과 완전히 동일하게 동작한다.

이처럼 yield from 키워드를 이해하고 있다면, 보다 깔끔하고 가독성 높은 코드 작성이 가능하다.

<br/>

쓸데없이 장황한(?) 예제를 들어가며 yield from에 대해 정말 간단히 알아보았다.

사실 개념을 정리하면서도 실제로 실무의 어떤 상황에서 적용될지 감이 잘 안잡힌다.

깊이있는 이해를 위해서는 실제 프로젝트에 적용하며 내공을 쌓아야할듯.
