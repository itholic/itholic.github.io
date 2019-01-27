---
title: "[kata][python] 숫자를 역순으로 출력"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 곱해진 결과에 포함된 숫자의 갯수

출처: <a href="https://www.acmicpc.net/problem/2742" target="_blank">백준 알고리즘 2742번 문제</a>

자연수 N을 받아 N부터 1까지 역순으로 출력


```
입력
    5

출력
    5
    4
    3
    2
    1
```

<br/>

## 내 풀이

```python
  1 import sys
  2
  3 N = int(sys.stdin.readline())
  4
  5 for i in range(N):
  6     print (N - i)
```

3번째 줄에서 N을 입력받고,

6번째 줄에서 iteration돌며 N부터 1까지 출력했다.

## 다른사람 풀이

```python
  1 print('\n'.join(map(str,range(int(input()),0,-1))))
```

input()으로 값을 받아 int로 형변환하고,

받은 값부터 0까지 내림차순으로 list를 만들었다.

그리고 이 list를 map함수를 통해 string으로 바꿔 새로운 리스트를 만들었고,

join 메소드를 사용해 리스트 요소를 개행문자 기준 문자열로 생성해 출력하였다.

## 분석

알고리즘 자체는 아주 단순하지만, 재밌는 코드가 있어서 가져왔다.

가장 안쪽에 데이터를 input받은 부분부터 역순으로 읽어 나오면, 전체 로직이 자연스레 읽힌다.

안쪽부터 사용된 함수를 순서대로 보면,

`input -> int -> range -> str -> map -> join -> print` 이다.

1. 입력받고(input), 

2. int로 변환해서(int) 역순으로 리스트를 만들고(range), 

3. 문자열로 바꾸어주는 메소드(str)를 각 요소에 적용해(map), 

4. 개행문자 기준으로 요소를 나누어 문자열을 만들고(join), 

5. 출력(print)

이런 방식이 오히려 가독성을 떨어뜨릴수도 있지만,

직관적이고 깔끔한 코드를 작성하기 위해 여러가지 표현 기법을 익혀둘 필요가 있을 것 같다.