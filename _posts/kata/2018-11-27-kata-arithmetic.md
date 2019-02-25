---
title: "[kata][python] 사칙연산"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 사칙연산

출처: <a href="https://www.acmicpc.net/problem/10869" target="_blank">백준 알고리즘 10869번 문제</a>

사용자 input으로 a, b 두 개의 값을 받아서

(a + b), (a - b), (a * b), (a / b), (a % b) 를 출력하는 예제이다.

데이터는 "a b" 와 같이 띄어쓰기 한개로 구분돼 들어온다.

## 내 풀이

```python
# -*- coding: utf-8 -*-

a, b = map(int, input().split(" "))

print (a + b)
print (a - b)
print (a * b)
try:
    print (int(a / b))
except ZeroDivisionError as zde:
    raise Exception(zde)
else:
    print (a & b)
```

앞선 kata에서 배운것처럼 map, split을 활용해 input을 받아오면서 바로 a, b 를 만들었다.

그리고 제수(분모)가 0인 경우의 예외를 처리하기 위해 try ~ except ~ else를 사용했다.


## 다른사람 풀이

```python
# -*- coding: utf-8 -*-

a, b = map(int, input().split())
print(a+b)
print(a-b)
print(a*b)
print(a//b)
print(a%b)
```

마찬가지로 input과 동시에 map, split을 사용해 a, b 를 만들었다.

따로 예외처리를 해주지 않고 그대로 출력했다.

a와 b의 몫을 구하는 과정에서 "/" 대신 "//"를 사용했다.

## 분석

가장 크게 배운점은, 

두 수를 나눈 몫만 구하고 싶을 때 "/" 대신 "//"를 쓰면 소숫점 아래를 버린다는 것이다.

그리고 다른 사람의 코드에서 예외처리를 해주지 않은 부분에 대해서는,

문제 조건을 다시보니 입력으로 두 "자연수" a, b 가 주어진다고 되어있었다.

따라서 0을 따로 처리할 필요가 없으므로 예외처리를 하는것이 오히려 성능 저하라는 것을 알게되었다.

클라이언트의 요구사항을 정확히 파악하고 예외처리를 해야한다는것을 배웠다.
