---
title: "[kata][python] 피보나치 수 구하기"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 피보나치 수 구하기

출처: <a href="https://www.acmicpc.net/problem/2747" target="_blank">백준 알고리즘 2747번 문제</a>

피보나치 수를 구하는 문제다.

n를 입력받아서 n번째 피보나치 수를 구한다.

참고로 피보나치수는 0번째부터 시작되므로, 

n+1번째 있는 숫자를 출력해야 n번째 피보나치 수가 나온다.

```
입력
    10

출력
    55
```

## 내 풀이1(시간초과)

```python
def fibonacci(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(int(input())))
```

재귀함수를 사용했다.

시간초과.


## 내 풀이2(런타임에러)

```python
n = int(input())
prev_two = [0, 1]

for i in range(2, n+1):
    result = sum(prev_two)
    prev_two = [prev_two[1], result]

print(result)
```

재귀함수를 반복문으로 바꿨다.

입력받은 숫자가 0이나 1일때 예외처리를 하지 않아 에러.

## 내 풀이3(정답)

```python
n = int(input())
prev_two = [0, 1]

if n in (0, 1):
    result = n
else:
    for i in range(2, n+1):
        result = sum(prev_two)
        prev_two = [prev_two[1], result]

print(result)
```

입력받은 숫자가 0이나 1일경우는 예외처리 해주었다.

## 분석

재귀함수는 가독성을 높여주지만, 성능상 이슈도 있고 recursive depth에 한계가 있으므로 상황을 잘 고려해 사용해야한다.

어차피 런타임시 잡아주긴 하지만 많은 케이스를 고려해 예외처리를 좀 더 꼼꼼하게 하자.
