---
title: "[python] 이중리스트 만들기(two-dimensional array)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 이중리스트 만들기

5행 10열짜리 이중리스트는 다음과 같이 만들면 된다.

모든 행과 열에 숫자 0을 넣는 예제.

```python
two_d_list = []
for _ in range(5):
    line = []
    for _ in range(10):
        line.append(0)
    two_d_list.append(line)
```

출력해보자.

```
[[0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]
```

리스트 안에 리스트가 들어간 구조이다.

`two_d_list[행번호][열번호]` 와 같은 형태로 접근하면 된다.

list comprehension을 이용해 더 파이썬스럽게 만드는 방법도 있다.

```python
two_d_list = [[0 for _ in range(10)] for _ in range(5)]
```

위 코드와 완전히 동일한 동작을 하면서 훨씬 직관적이고 깔끔하다.
