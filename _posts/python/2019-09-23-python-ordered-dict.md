---
title: "[python] OrderedDict & Comprehension"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# OrderedDict

딕셔너리에 데이터를 넣을때, 들어간 순서를 보장해줄까?

파이썬 2.7 버전에서 테스트해보자.

```python
>>> d = dict()
>>> d['a'] = 'app'
>>> d['b'] = 'bow'
>>> d['c'] = 'cow'
>>> d
{'a': 'app', 'c': 'cow', 'b': 'bow'}
```

집어 넣을때는 a, b, c 순서로 넣었는데,

출력해보니 a, c, b 순서로 저장되어있다.

근데 이렇게 데이터가 적을때는 운좋게 넣은 순서대로 들어갈수도 있다.

좀 더 많은 데이터로 실험해보자.

```python
>>> keys = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> vals = ['app', 'bow', 'cow', 'doc', 'err', 'fly', 'gpu']
>>> d = {key: val for key, val in zip(keys, vals)}
>>> d
{'a': 'app', 'c': 'cow', 'b': 'bow', 'e': 'err', 'd': 'doc', 'g': 'gpu', 'f': 'fly'}
```

이번엔 표현식을 사용했다.

데이터가 많으니 순서가 뒤죽박죽인것이 더 명확히 드러난다.

데이터를 넣은 순서대로 딕셔너리에 저장하려면 어떻게 해야할까?

collections 모듈에 있는 OrderedDict라는 자료형을 사용하면 된다.

그냥 예제를 보자.

```python
>>> from collections import OrderedDict
>>> d = OrderedDict()
>>> d['a'] = 'app'
>>> d['b'] = 'bow'
>>> d['c'] = 'cow'
>>> d
OrderedDict([('a', 'app'), ('b', 'bow'), ('c', 'cow')])
```

간단하다. dict() 대신 OrderedDict()를 사용해주면 된다.

이번엔 표현식으로 OrderedDict를 만들어보자.

```python
>>> from collections import OrderedDict
>>> keys = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> vals = ['app', 'bow', 'cow', 'doc', 'err', 'fly', 'gpu']
>>> d = OrderedDict({key: val for key, val in zip(keys, vals)})
{'a': 'app', 'c': 'cow', 'b': 'bow', 'e': 'err', 'd': 'doc', 'g': 'gpu', 'f': 'fly'}
```

OrderedDict를 사용했는데도 순서가 보장되지 않았다. 왜그럴까?

OrderedDict 표현식은 `key: val` 대신 `(key, val)` 의 형태를 취해야한다.


```python
>>> from collections import OrderedDict
>>> keys = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> vals = ['app', 'bow', 'cow', 'doc', 'err', 'fly', 'gpu']
>>> d = OrderedDict((key, val) for key, val in zip(keys, vals))
OrderedDict([('a', 'app'), ('b', 'bow'), ('c', 'cow'), ('d', 'doc'), ('e', 'err'), ('f', 'fly'), ('g', 'gpu')])
```

들어간 순서대로 잘 정렬이 되었다.

참고로 파이썬 3.6 버전부터는 자동으로 정렬을 해주므로 굳이 OrderedDict를 사용할 필요는 없다.

하지만 하위 호환성이 필요하고, 데이터의 순서가 중요한 상황인 경우는 OrderedDict를 사용해 순서를 보장해야한다.

