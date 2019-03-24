---
title: "[python] reverse, reversed 차이"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 reverse, reversed의 차이

파이썬에서 리스트의 요소를 뒤집을때 reverse, reversed를 사용한다.

이 두개의 차이에 대하여 간단하게 알아보자.


#### reverse

1. reverse는 list타입에서 제공하는 함수이다.

```python
l = ['a', 'b', 'c']
t = ('a', 'b', 'c')
d = {'a': 1, 'b': 2, 'c': 3}
s = 'abc'

l.reverse()  # list의 순서를 뒤집어줌
t.reverse()  # AttributeError: 'tuple' object has no attribute 'reverse'
d.reverse()  # AttributeError: 'dict' object has no attribute 'reverse'
s.reverse()  # AttributeError: 'str' object has no attribute 'reverse'
```

2. reverse는 값을 반환하지 않고, 단순히 해당 list를 뒤섞어준다.

```python
l = ['a', 'b', 'c']
l_reverse = l.reverse()

print(l_reverse)  # None
print(l)  # ['c', 'b', 'a']
```


#### reversed

1. reversed는 내장함수로, list에서 제공하는 함수가 아니다.

```python
l = ['a', 'b', 'c']
t = ('a', 'b', 'c')
d = {'a': 1, 'b': 2, 'c': 3}
s = 'abc'

reversed(l)  # <listreverseiterator object at 0x101053c10>
reversed(t)  # <reversed object at 0x101053b50>
reversed(d)  # TypeError: argument to reversed() must be a sequence
reversed(s)  # <reversed object at 0x101053c10>
```

보다시피 딕셔너리는 시퀀셜한 타입이 아니므로 지원하지 않는다.

즉, l[0], l[1] 과 같이 순차적인 인덱스로 접근할 수 없기떄문에 지원하지 않는다.


2. reversed는 'reversed' 객체를 반환한다.

```python
l = ['a', 'b', 'c']
t = ('a', 'b', 'c')
s = 'abc'

reversed(l)  # <listreverseiterator object at 0x101053c10>
reversed(t)  # <reversed object at 0x101053b50>
reversed(s)  # <reversed object at 0x101053c10>
```

tuple과 str의 경우 'reversed' 객체를 반환하는것을 볼 수 있다.

하지만 list의 경우 특이하게 'listreverseiterator'를 반환하고있다.

사용 방법에 차이는 없으므로 크게 신경쓰지 않아도 된다.

(혹시 유의미한 차이점에 대해 알고계신분이 있다면 댓글 달아주시면 감사하겠습니다)

reversed 객체를 tuple 혹은 list로 바꾸어 사용해주려면 다음과 같이 하면 된다.

```python
l = ['a', 'b', 'c']
t = ('a', 'b', 'c')

list(reversed(l))  # ['c', 'b', 'a']
tuple(reversed(t))  # ('c', 'b', 'a')
```

물론, list로 만든 listreverseiterator 객체를 반드시 list로 만들어야 되는 것은 아니고,

tuple로 만든 reversed 객체를 반드시 tuple로 만들어야하는건 아니다.

문자열로 만들려면 굳이 list나 tuple로 바꿀 필요 없이 join을 통해 요소들을 연결해주면 된다.

```python
l = ['a', 'b', 'c']

''.join(reversed(l))  # 'cba'
```
