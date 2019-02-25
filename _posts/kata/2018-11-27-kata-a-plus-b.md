---
title: "[kata][python] A + B"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# A + B

출처: <a href="https://www.acmicpc.net/problem/1000" target="_blank">백준 알고리즘 1000번 문제</a>

사용자 input으로 a, b 두 개의 값을 받아서 a + b 를 출럭하는 간단한 문제이다.

데이터는 "a b" 와 같이 띄어쓰기 한개로 구분돼 들어오고, 두 값을 더한 값을 출력하면 된다.

## 내 풀이

```python
# -*- coding: utf-8 -*-

input_data = input()
a, b = input_data.split(" ")

print (int(a) + int(b))
```

input으로 받은 데이터를 'input_data' 변수에 넣고,

input_data를 다시 공백 기준으로 잘라서 각각 a, b 변수에 넣었다.

그리고 print를 하면서 동시에 자료형 변환을 해주었다.

## 다른사람 풀이

```python
# -*- coding: utf-8 -*-

a, b = map(int, input().split(" "))

print (a + b)
```

map과 split을 이용해 데이터를 받음과 동시에 공백 기준으로 잘라서 int함수를 적용해 형변환까지 처리했다.

그리고 처리된 a, b 를 출력했다.

## 분석

수행 속도를 보니 성능상 차이는 없지만, (실제로는 차이가 있을 것 같은데, 너무 짧은 코드라서 속도 차이가 없는 것 처럼 보인 것일수도 있다)

내가 짠 코드보다 예시로 나와있는 코드가 일단 라인수도 적은데다가 가독성도 좋은 것 같다.

무엇보다 'input_data' 와 같이 애매한 이름의 변수를 사용하지 않았다는점이 가장 주요한 차이인 것 같다.
