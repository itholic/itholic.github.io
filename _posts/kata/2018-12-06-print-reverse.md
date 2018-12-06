---
title: "[kata][python] 숫자를 역순으로 출력 (함수형 프로그래밍 혀끝만 대보기)"
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

사실 알고리즘이라고 하기도 부끄러운 엄청 간단한 로직이지만, 

함수형 프로그래밍에 관심이 많은 요즘 참고될만한 괜찮은 코드가 있어서 가져와봤다.

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


글의 서두에 함수형 프로그래밍을 공부하는데에 참고될만한 코드가 있어서 가져와봤다고 했었다.

이게 무슨말인지 다른사람의 코드를 간단하게 분석해보자.

한 줄에 모든 메소드를 몰아 넣었지만, 데이터의 흐름대로 이해하기 용이하게 정렬되어있다.

가장 안쪽에 데이터를 input받은 부분부터 역순으로 읽어 나오면, 전체 로직이 자연스레 읽힌다.

안쪽부터 사용된 함수를 순서대로 보면, 

`input -> int -> range -> str -> map -> join -> print` 이다.

1. 입력받고(input), 

2. int로 변환해서(int) 역순으로 리스트를 만들고(range), 

3. 문자열로 바꾸어주는 메소드(str)를 각 요소에 적용해(map), 

4. 개행문자 기준으로 요소를 나누어 문자열을 만들고(join), 

5. 출력(print)

코드가 직관적으로 변하는 것 뿐 아니라,

각 함수들은 입력받은 인자 외에 외부 변수를 사용하지 않는 순수함수로, 

같은 입력에 대한 같은 결과를 보장하기 때문에 예상치못한 부작용을 줄이는데에도 효과적이다.
