---
title: "[kata][python] 단어의 갯수"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 문자열에 속한 단어의 갯수는?

출처: <a href="https://www.acmicpc.net/problem/1152" target="_blank">백준 알고리즘 1152번 문제</a>

영어 대소문자와 띄어쓰기로 이루어진 문자열에 포함된 단어의 갯수는?

단어는 띄어쓰기 한 개로 구분된다.


```
입력
    The Curious Case of Benjamin Button

출력
    6
```    

## 내 풀이

```python
  1 import sys
  2
  3 S = sys.stdin.readline()
  4
  5 if S.strip() == "":
  6     word_count = 0
  7 else:
  8     word_count = 1
  9     for data in S.strip():
 10         if data == " ":
 11             word_count += 1
 12
 13 print(word_count)
```

입력받은 문자열의 양쪽 공백을 지우고,

그 값이 공백이면 단어가 없는 것이므로 word_count를 0으로 초기화한다.

그렇지 않은 경우는 우선 단어가 최소 1개 등장한다는 뜻이므로 word_count를 1로 초기화하고,

입력받은 문자열을 iteration하며 공백이 나올때마다 단어 갯수를 하나씩 더해준다.

이미 양쪽 공백을 strip한 상태이므로, 공백이 있다는 것은 다음에 단어가 하나 더 등장한다는것을 의미하기 때문이다.


## 다른사람 풀이

```python
print(len(input().split()))
```
입력받은 문자열을 split해서 배열로 만들고, 배열의 길이를 구했다.

## 분석

이번 문제는 개인적인 사정으로 좀 급하게 풀었다.

문제 카테고리 자체가 배열이었는데, 너무 급하게 풀다보니 중요한 힌트를 간과했다.

공백을 기준으로 문자열을 잘라서 배열의 길이를 구하면 끝나는 문제였는데, 다시 봐도 아쉽다.

정말 급한 약속이 생겨서 나가기 직전에 급하게 풀다보니까 이렇게 풀면 아무 의미가 없지 않을까 생각했는데,

오히려 '급할수록 돌아가라'는 말이 피부로 와닿는 나름 귀중한 경험이 되었다.

급할수록 더욱 원리에 입각해서 차분히 생각하다보면, 시간을 더욱 절약하고 효율적인 코딩을 할 수 있지 않을까하는 생각이 들었다.
