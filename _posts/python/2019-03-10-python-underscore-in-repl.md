---
title: "[python] REPL(인터프리터)에서 언더스코어의 활용"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# _ in REPL

파이썬에서 언더스코어는 일반적으로 다음과 같이 특정 리턴값을 무시하거나,

```python 
import random


def return_abc():
    a = random.random()
    b = random.random()
    c = random.random()
    return a, b, c

_, _, c = return_abc()
print(c)
```

다음과 같이 클래스내에서 특정 변수나 함수를 protected 혹은 private로 규정하고싶을때 사용한다.

```python
class MyClass:
    _protected_var = None
    __private_var = None

    def _protected_method():
        pass

    def __private_method():
        pass
```

하지만 REPL(대화형 인터프리터)에서는 바로 직전 출력된 결과를 저장하는 역할을 한다.

```
>>> 1 + 2
3
>>> _
3
>>> _ * 10
30
>>> _
30
```

별건 아니지만, 그냥 부스러기같은 팁으로 정리해보았다.
