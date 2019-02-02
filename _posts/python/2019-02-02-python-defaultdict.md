---
title: "[python] defaultdict"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# defaultdict

python의 collections 모듈에는 defaultdict라는 기능이 있다.

defaultdict는 이름 그대로 기본값을 지정한 딕셔너리인데, 이게 무슨말일까?

일반 딕셔너리의 경우, 미리 삽입하지 않은 key를 호출하면 다음과 같이 에러가 난다.

```python
>>> n_dict = dict()
>>> n_dict["a"]

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'a'
```

"a" 라는 키의 값을 넣어준적이 없기때문에, 당연히 에러가 난다.

물론 다음과 같이 setdefault를 사용해 호출과 동시에 선언도 가능하다.

```python
>>> n_dict = dict()
>>> n_dict.setdefault("a", 0)
0
>>> n_dict
{'a': 0}
```

이 방식을 사용하면 key를 넣을때마다 setdefault 함수를 써주어야한다.

setdefault를 사용하지 않고 호출과 동시에 미리 지정한 기본값이 할당되도록 선언할수는 없을까?

이럴때 defaultdict를 사용한다.

defaultdict를 활용해 다음과 같이 기본값을 'int' 로 선언해주고,

기존에 없던 key를 호출하면 다음과 같이 해당 key가 0으로 자동 초기화된다.

```python
>>> from collections import defaultdict
>>> d_dict = defaultdict(int)
>>> d_dict["a"]
0
>>> d_dict
defaultdict(<class 'int'>, {'a': 0})
```

심지어 미리 선언하지 않은 key에 값을 더해주는 것도 가능하다.

```python
>>> d_dict = defaultdict(int)
>>> d_dict["a"] += 10
10
>>> d_dict
defaultdict(<class 'int'>, {'a': 10})
```

다음과 같이 lambda 식을 사용해 원하는 초기값을 지정할수도 있다.

```python
>>> d_dict = defaultdict(lambda: 'default value')
>>> d_dict["a"]
'default value'
```
