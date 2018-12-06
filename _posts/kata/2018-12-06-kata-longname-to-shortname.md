---
title: "[kata][python] 긴 이름을 짧은 이름으로 바꾸기"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 긴 이름을 짧은 이름으로 바꾸기

출처: <a href="https://www.acmicpc.net/problem/2902" target="_blank">백준 알고리즘 2902번 문제</a>

하이픈으로 구분된 긴 이름을 짧은 이름으로 바꿔라

```
입력
    Knuth-Morris-Pratt

출력
    KMP
```

<br/>

## 내 풀이

```python
  1 import sys
  2
  3 long_name_list = sys.stdin.readline().rstrip().split("-")
  4 short_name = "".join([long_name[0] for long_name in long_name_list])
  5
  6 print(short_name)
```

3번째 줄에서 긴 이름을 입력받고, 

하이픈(-)을 기준으로 split해서 list를 만들었다.

4번째 줄에서 각 요소의 첫 번째 string만 가져와 이어 붙였다.

## 다른사람 풀이

```python
  1 print(''.join(i for i in input() if 64<ord(i)<91))
```

input으로 값을 받고, 

ASCII코드가 64에서 91 사이인 값에 대해서만 이어붙여 출력했다.

참고로 ASCII코드 65는 A, 90은 Z이다.

## 분석

분명 문제에 하이픈 뒤의 첫 글자는 무조건 대문자라고 했는데,

ASCII코드를 활용한 문제 해결방법을 떠올리지 못했다.

무조건 돌아가는것만 중요한게 아니라,

요구사항에 제시되어있는 힌트를 잘 활용하는것도 프로그래머의 능력이다.

아직 갈 길이 멀다는걸 느꼈고,

대문자를 활용한다고 생각하니 string 모듈을 활용한 다음과 같은 풀이도 떠올랐다.

```python
  1 import sys
  2 import string
  3
  4 print("".join([case for case in sys.stdin.readline().rstrip() if case in string.ascii_uppercase]))
```

string 모듈의 ascii_uppercase에는 대문자 A부터 Z까지가 담겨있다.

이를 활용해 받은 문자열에서 대문자를 골라내 이어붙여 출력하는 방식이다.

근데 기존 풀이에 비해 메모리도 10%가량 많이 먹고, 시간은 거의 2배가 소요된다;

string 모듈에 저장된 ascii 값들을 활용하는게 통상적으로 사용되는 방식도 아니고,

그냥 이런 방법도 있다 정도만 알고 넘어가는게 좋을 것 같다.

참고로 내가 풀이한 방식과 다른 사람의 방식에서 메모리 사용량과 성능의 차이는 없었다.

아마 코드가 워낙 짧아서 그런걸지도?
