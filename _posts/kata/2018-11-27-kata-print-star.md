---
title: "[kata][python] 별 찍기 - 4"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 별 찍기 - 4

출처: <a href="https://www.acmicpc.net/problem/2441" target="_blank">백준 알고리즘 2441번 문제</a>

사용자 input으로 정수 N을 받아서 첫 째 줄부터 N번째 줄까지 별을 출력하는 예제이다.

N이 5일 경우 출력은 다음과 같다.

```
*****
 ****
  ***
   **
    *
```

## 내 풀이

```python
# -*- coding: utf-8 -*-

line = int(input())

for i in range(line):
    num_star = line - i
    num_whitespace = i
    print ( (" " * num_whitespace) + ("*" * num_star) )
```

input으로 받은 숫자를 line 변수에 넣고, line 수만큼 for문을 돌렸다.

출력할 별의 갯수와 출력할 공백의 갯수를 각각 num_star, num_whitespace로 정의하고,

각각의 변수에 "\*"(별)과 " "(공백)을 곱해 출력했다.

## 다른사람 풀이

```python
  1 # -*- coding: utf-8 -*-
  2
  3 n = int(input())
  4 for i in range(n):
  5     print(" "*i, end='')
  6     print("*"*(n-i))
```

사실 대부분이 for문 내에서 `print(((" ")*i)+("*"*(n-i)))` 과 같은 형태로 처리했다. (n은 본인 예제에서 line과 같음)

즉, 변수를 굳이 따로 두지 않고 print하면서 한 번에 처리했다. 

근데 이 케이스는 특이하게 5번째 줄에서 print함수 안에 `end=''` 라는 문법이 들어가서 가져와봤다.

print 함수의 두 번째 인자로 end를 주게되면, 개행을 하는 대신 해당 문자열이 들어온다.

그래서 출력할때 5번쨰 줄과 6번째 줄의 출력이 개행되지 않고 한 줄에 붙어서 출력된다.

## 분석

대부분의 사람들은 for문 내에서 따로 변수를 만들지 않고, 주어진 변수를 사용했다.

이 부분은 어떤것이 더 나은 방법인지 상황에따라 다를 것 같아서 우선은 참고용으로만 생각해둬야겠다.

그리고 print문에 end라는 인자를 주어 개행 대신 해당 문자를 줄 수 있다는 사실을 처음 알았다.
