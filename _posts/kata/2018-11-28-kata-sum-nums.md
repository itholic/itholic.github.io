---
title: "[kata][python] 숫자의 합"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 숫자의 합

출처: <a href="https://www.acmicpc.net/problem/11720" target="_blank">백준 알고리즘 11720번 문제</a>

첫 번째 줄에서 숫자의 개수 N을 받는다.

두 번째 줄에서 공백 없이 이어져있는 N개의 숫자를 받는다.

공백 없이 이어진 N개 숫자의 합을 출력한다.

```
입력
    11
    10987654321

출력
    46
```

## 내 풀이

```python
  1 import sys
  2
  3 N = int(sys.stdin.readline().rstrip())
  4 num = sys.stdin.readline().rstrip()
  5
  6 sum_num = 0
  7 for i in range(N):
  8     sum_num += int(num[i])
  9
 10 print(sum_num)
```

3, 4 번 라인에서 각각 숫자의 갯수와 공백 없이 이어진 숫자를 받았다.

6번 라인에서 숫자의 합을 저장할 sum_num을 0으로 초기화한다.

문자열은 iterable하므로, 한 문자열씩 접근해 int로 변경한 후 sum_num에  더해준다.

## 다른사람 풀이

```python
  1 c = int(input())
  2 n = input()
  3 l = list(n)
  4 nl = [int(i) for i in l]
  5 print(sum(nl))
```

1,2 번 라인에서 인자를 받았다.

3번 라인에서 입력받은 문자열을 리스트로 생성했다.

3번 라인에서 생성한 리스트의 모든 값을 int로 바꾸어, nl이라는 리스트에 다시 저장했다.

리스트의 합을 sum으로 구해 출력했다.


## 분석

다른사람의 풀이는 변수명을 한글자 변수로 알아보기 어렵게 썼다는 점에서 개선점이 보인다.

그리고 map함수를 활용하거나, 그렇지 않더라도 3, 4 번 라인을 한 줄로 간결하게 표현할 수 있었을텐데 그점도 좀 아쉽다.

하지만 리스트로 변환해 sum 메소드를 적용했다는 점이 내가 해결한 방법과 다른 부분이라서 주목했다.

문자열을 그대로 iteration하는 것이 왠지 좀 더 효율적일 것 같지만, 효율성을 떠나 나름 신선했다.

그리고 이 문제만을 떠나서, 문자열을 처리할때 리스트로 만들어서 처리하는 부분에 대한 가능성이 하나 열린 셈이다.
