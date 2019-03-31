---
title: "[python] range, xrange 차이"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 range, xrange차이

시작하기 전에,

파이썬3에는 xrange라는 키워드가 따로 없고, range만 존재한다.

python3에서 xrange를 사용하려고하면, 정의되지 않았다는 에러가 출력된다.

```python
# python3
>>> r = range(10)
>>> type(r)
<class 'range'>
>>> xr = xrange(10)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'xrange' is not defined
```

그 이유는 파이썬3부터는 range가 내부적으로 xrange로 동작하도록 바뀌었기 때문이다.

즉, range를 없애고 xrange만 남긴 것이다.(range가 내부적으로 xrange로 동작하므로)

<br/>

그럼, 파이썬2에서 둘의 차이는 무엇일까?

우선 range 객체를 만들어보자.

```python
# python2
>>> r = range(10)
>>> type(r)
<type 'list'>
>>> r
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

range 객체를 만들고 타입을 확인해보니 'list'로 나온다.

실제로 내용을 출력해봐도 0부터 9까지 숫자가 담긴 list가 출력된다.

즉, 다음 두 개의 코드는 완전히 동일하다.

```python
# python2
for i in range(10):
    print(i)
```

```python
# python2
for i in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]:
    print(i)
```

이번엔 xrange를 만들어보자.

```python
# python2
>>> xr = xrange(10)
>>> type(xr)
<type 'xrange'>
>>> xr
xrange(10)
```

xrange 객체를 만들고 타입을 확인해보니 'xrange'로 나온다.

실제로 내용을 출력해봐도 xrange(10) 이라고 나올 뿐이다.

xrange는 generator(혹은 iterator)의 일종이라고 이해하면 된다.

사실 엄밀히 따지면 generator와 iterator는 다른 개념이지만,

실제로 파이썬 커뮤니티에서 iterator와 generator를 그렇게 깐깐하게 따지지 않는다.

정 따지고싶다면, 그냥 xrange는 'xrange' 그 자체로 이해하면 되며,

next() 메소드를 통해 <a href="https://itholic.github.io/python-lazy-evaluation/" target="_blank">Lazy Evaluation</a> 방식으로 값을 하나씩 제공하는 객체로 이해하면 된다.

<br/>

어쨌든 중요한건, range에 비해 메모리 효율이 좋다는 사실을 알고있으면 된다.

실제로 sys.getsizeof 함수를 이용해 range와 xrange의 메모리 사용량을 비교해보자.

```python
# python2
>>> import sys
>>> r = range(10000)
>>> sys.getsizeof(r)
80072
```

range를 통해 10000개의 요소를 담은 list를 만들었을때,

메모리 사용량은 80072이다.

```python
# python2
>>> import sys
>>> xr = range(10000)
>>> sys.getsizeof(xr)
40
```

xrange의 경우에는 똑같은 갯수의 아이템을 가졌음에도 불구하고,

메모리 사용량은 단 40에 그친다.

이 이유는 앞에서 언급한 <a href="https://itholic.github.io/python-lazy-evaluation/" target="_blank">Lazy Evaluation</a>에 대한 개념이 있으면 쉽게 이해가 가능하다.
