---
title: "[kata][python] 단지 번호 붙이기 (다차원 행렬 탐색문제)"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 단지 번호 붙이기

출처: <a href="https://www.acmicpc.net/problem/2667" target="_blank">백준 알고리즘 2667번 문제</a>

숫자 1과 0으로 이루어진 N x N 행렬이 있다.

1은 가구가 존재하는 블록, 0은 가구가 존재하지 않는 블록이라고 생각하자.

가구가 상하좌우로 붙어있는 경우, 같은 단지로 판정한다. (대각선은 인정하지 않는다)

주어진 N x N 행렬에 포함된 단지의 갯수와, 각 단지에 포함된 가구의 갯수를 출력해보자. (가구의 갯수는 오름차순으로)

입력은 N x N행렬의 'N', 이어서 N개의 행이 주어진다.

```
입력
    7
    0110100
    0110101
    1110101
    0000111
    0100000
    0111110
    0111000

출력
    3
    7
    8
    9
```

## 내 풀이

```python
  1 # -*- coding: utf-8 -*-
  2
  3 danji_num = 0
  4 danji_dic = dict()
  5 n = int(input())
  6
  7 lists = [[int(block) for block in input()] for _ in range(n)]
  8
  9 def check_around(i, j):
 10     """주어진 인덱스의 상하좌우를 모두 뒤져서 1이 발견될때마다 단지내 가구수를 1개씩 증가시킨다
 11     한 번 방문한 인덱스는 0으로 체크해서 다시 방문하지 않도록 조치한다"""
 12     if i != 0:
 13         # 상
 14         if lists[i-1][j] == 1:
 15             danji_dic[danji_num] += 1
 16             lists[i-1][j] = 0
 17             check_around(i-1, j)
 18     if i != n-1:
 19         # 하
 20         if lists[i+1][j] == 1:
 21             danji_dic[danji_num] += 1
 22             lists[i+1][j] = 0
 23             check_around(i+1, j)
 24     if j != 0:
 25         # 좌
 26         if lists[i][j-1] == 1:
 27             danji_dic[danji_num] += 1
 28             lists[i][j-1] = 0
 29             check_around(i, j-1)
 30     if j != n-1:
 31         # 우
 32         if lists[i][j+1] == 1:
 33             danji_dic[danji_num] += 1
 34             lists[i][j+1] = 0
 35             check_around(i, j+1)
 36
 37 for i in range(n):
 38     for j in range(n):
 39         if lists[i][j] == 1:
 40             danji_num += 1  # 단지를 발견했으므로 danji_num 1개 증가
 41             danji_dic[danji_num] = 1  # 단지별 가구수를 저장하기위해 danji_dic에 초기값 1 할당(방금 발견한 가구를 포함시킨것)
 42             lists[i][j] = 0  # 이미 방문한 가구는 0으로 체크해서 다시 방문하지 않도록 조치
 43             check_around(i, j)  # 발견한 단지의 상하좌우 전부 뒤지기
 44
 45 print(danji_num)
 46 for key in sorted(danji_dic, key=lambda x: danji_dic[x]):
 47     print(danji_dic[key])
```

7번째 줄에서 우선 입력받은 자료를 활용해 n * n 배열을 만들어준다.

9번째 줄에 선언한 `check_around` 는 주어진 인덱스를 기준으로 상하좌우의 배열을 체크하는 함수이다.

좀 어지러워보이지만 로직이 복잡하지 않으므로 찬찬히 보면 금방 이해될것이다.

상하좌우 체크시, 어느 한쪽이 벽에 막혀있을 경우 인덱스에러가 날 수 있으므로 각 상황에 맞는 조건을 걸어줬다.

상하좌우에 1이 존재하는 경우는 해당 단지의 가구수를 하나 증가시키고, (`danji_dic[danji_num] += 1`)

체크한 배열을 다시 카운팅하지 않도록 0으로 체크한다. (`lists[행][열] = 0`)

그리고 상하좌우에 1이 나타나지 않을때까지 계속 재귀호출하며 같은 동작을 반복한다.

이제 함수를 호출하는 부분을 보자.

37~43줄을 보면 주어진 행렬을 한 개씩 돌며 숫자 1이 발견되면 `check_around` 함수에 해당 인덱스를 넘겨주었다.

이 때, 단지번호와 그에 속한 가구수를 기록하기위해 `danji_dic` 이라는 딕셔너리를 이용했다.

46~47줄에서는 단지번호와 가구수를 저장한 딕셔너리를 value기준으로 오름차순 정렬 후 value를 순차적으로 출력했다.

(참고로 input()대신 sys.stdin.readline().rstrip()을 사용하면 더 빠르다)

## 다른사람 풀이

```python
  1 import sys
  2
  3 dx = [-1, 0, 1, 0]
  4 dy = [0, 1, 0, -1]
  5 n = int(sys.stdin.readline())
  6 a = [list(sys.stdin.readline()) for _ in range(n)]
  7 cnt = 0
  8 apt = []
  9
 10 def dfs(x, y):
 11     global cnt
 12     a[x][y] = '0'
 13     cnt += 1
 14     for i in range(4):
 15         nx = x + dx[i]
 16         ny = y + dy[i]
 17         if nx < 0 or nx >= n or ny < 0 or ny >= n:
 18             continue
 19         if a[nx][ny] == '1':
 20             dfs(nx, ny)
 21
 22 for i in range(n):
 23     for j in range(n):
 24         if a[i][j] == '1':
 25             cnt = 0
 26             dfs(i, j)
 27             apt.append(cnt)
 28
 29 print(len(apt))
 30 apt.sort()
 31 for i in apt:
 32     print(i)
```

해결 논리는 같지만, 코드 가독성부분에서 훨씬 더 낫다고 느낀다.

dx, dy라는 리스트를 만들어서, 해당지점을 기준으로 상하좌우 탐색을 하겠다는 의도를 보다 명확히 드러냈다.

굳이 딕셔너리를 만들지 않고, 리스트에 각 단지의 가구수를 집어넣었다.

이렇게하면 리스트의 길이가 곧 단지의 갯수이며, 리스트를 정렬해서 출력하기만 하면 끝이다.

## 분석

문제를 풀며 크나큰 자괴감이 들었는데,

왜냐면 이건 1996년 초등부 정보올림피아드 1번 문제다.

물론 내가 풀지 못한것은 아니지만 누군가는 이걸 초등학생때 이미 정복했다는 것이다.

사실 정보올림피아드라는걸 어떤 실력있는 선임님을 통해 처음 알았는데, 

그분도 중학생때부터 대회에 출전했었다고 하니 역시 대단하다는 생각이 든다.

<br/>

어쨌든 코드적인 측면에서는 다차원배열에대한 시야가 한 층 더 넓어지는 계기가 된 것 같아 좋았고,

최근 공부했었던 list comprehension이나 sorted, lambda등을 적극 활용해 문제를 풀게되어 뿌듯했다.

평소에 이런 실생활 접목(?) 문제를 푸는데 있어서 지레 겁을 많이 먹었었는데,

문제 앞에서 쫄지만 않고 차분히 풀면 어떤 문제든 정복하지 못할 문제는 없는 것 같다.

다만 코드 가독성, 성능, 효율성등의 면에서 차이가 있겠지만, 이런 부분은 어차피 꾸준히 메꿔나가야하는 부분이다.
