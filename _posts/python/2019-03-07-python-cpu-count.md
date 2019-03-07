---
title: "[python] cpu 개수 확인하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# cpu 개수 확인하기

python에서 여러가지 이유로 cpu의 개수를 확인해야할 상황이 있다.

이는 os 모듈의 `cpu_count` 를 통해 알아낼 수 있다.

```python
import os

os.cpu_count()  # 2
```

`cpu_count` 는 multiprocessing 모듈에도 있다.

참고로 python 3.4 미만에서는 multiprocessing 모듈에'만' 있으니 주의하자.

3.4 미만에서는 os 모듈에 `cpu_count` 메서드가 없다.

```python
import multiprocessing

multiprocessing.cpu_count()  # 2
```

사람마다 이를 활용하는 방법은 다르겠지만,

나같은 경우는 쓰레드 몇 개를 한 번에 돌릴지 가늠하기 위해 사용한다.

보통 cpu 개수의 두 배 정도를 한 번에 돌린다.
