---
title: "[kata][python] 진짜 일곱 난장이를 찾아라!"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 진짜 일곱난장이를 찾아라!

출처: <a href="https://www.acmicpc.net/problem/2309" target="_blank">백준 알고리즘 2309번 문제</a>

백설공주가 일과를 마치고 돌아왔는데 난쟁이가 일곱명이 아닌 아홉명이었다.

이들은 전부 자신이 진짜 일곱 난쟁이중 하나라고 우기고 있었다.

백설공주는 일곱 난쟁이의 키를 모두 합하면 100이라는 사실을 알고있다.

난쟁이의 키 9개가 입력으로 주어졌을때, 진짜 난쟁이의 7명의 키를 오름차순으로 출력하라.

```
입력
    20
    7
    23
    19
    10
    15
    25
    8
    13

출력
    7
    8
    10
    13
    19
    20
    23
```

## 내 풀이

```python
  1 import sys
  2
  3 height_list = []
  4
  5 for _ in range(9):
  6     height_list.append(int(sys.stdin.readline()))
  7
  8 for i in range(len(height_list)):
  9     for j in range(i, len(height_list)-1):
 10         tmp_height = list(height_list)
 11         del tmp_height[i], tmp_height[j]
 12
 13         if sum(tmp_height) == 100:
 14             tmp_height.sort()
 15
 16             for height in tmp_height:
 17                 print(height)
```

(3~6) 9명 난쟁이의 키를 저장할 리스트 height_list를 만들어, 입력으로 받아 추가하였다.

(8~11) 9명의 난쟁이 중 서로 다른 조합 2명씩 뽑아서, 그 두명의 키를 지워본다.

(13~17) 지우고 남은 7명의 키를 더해서 100이라면, 오름차순으로 정렬 후 출력한다.

del 명령을 쓰면 리스트에서 값이 지워지므로,

원본 데이터를 지우지 않기위해 shallow copy를 사용해 tmp_height를 만들어 계산하였다.


## 다른사람 풀이

```python
  1 tall = []
  2 for _ in range(9):
  3     tall.append(int(input()))
  4
  5 tall.sort()
  6
  7 total = sum(tall)
  8
  9
 10 for i in range(0,9):
 11     for j in range(i+1,9):
 12         if total - tall[i] - tall[j] == 100:
 13             for k in range(9):
 14                 if i == k or j == k:
 15                     continue
 16                 print(tall[k])
```

(1~3) 마찬가지로 9명 난쟁이의 키를 리스트로 받았다.

(7) 키의 전체 합을 구했다.

(10~12) 마찬가지로 서로 다른 조합을 2명씩 뽑았지만,

리스트에서 지운 것이 아니라 해당 인덱스에 해당하는 난쟁이 키를 전체 키의 합에서 지웠다.

(13~16) 특정 두 난장이의 키를 지웠을때의 토탈이 100이라면,

해당 난쟁이의 인덱스를 제외한 나머지 7명의 인덱스에 해당하는 키를 출력한다.

## 분석

상대적으로 간단한 문제여서 특별히 복잡한부분은 없었다.

그래서 여러 코드를 보기보다는 채점 현황표의 맨 꼭대기에 있는 사람의 코드를 가져와봤다.

현황표 위쪽에 있을수록 속도라던지 메모리 활용 부분에서 효율적이라는 것을 의미하는 듯 하다.

비교해보니, 내 방식은 리스트의 값을 복사하고 지우는 과정에서 상대적으로 느려진것으로 보인다.

복사, 삭제, 추가 등의 작업은 단순 조회보다 상대적으로 값비싸니 당연한 결과이다.

개념적으로는 알고 있었던 것이지만,

성능 차이에 대해 실제로 체감할 경험이 없었는데 좋은 경험이 된 것 같다.

코드 리팩토링시 이러한 부분을 염두에 두어야겠다.