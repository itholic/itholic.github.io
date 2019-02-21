---
title: "[kata][python] 프로그래머스 - 더 맵게"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 더 맵게

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42626" target="_blank">프로그래머스 - 더 맵게</a>

## 문제

매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다.

모든 음식의 스코빌 지수를 K 이상으로 만들기 위해,

Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

```
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.

Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때,

모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.


### 제한 사항

scoville의 길이는 1 이상 1,000,000 이하입니다.

K는 0 이상 1,000,000,000 이하입니다.

scoville의 원소는 각각 0 이상 1,000,000 이하입니다.

모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.


### 입출력 예

```
scoville: [1, 2, 3, 9, 10, 12]
K: 7
return: 2
```

### 입출력 예 설명

스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.

```
새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]
```

스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.

```
새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
가진 음식의 스코빌 지수 = [13, 9, 10, 12]
```

모든 음식의 스코빌 지수가 7 이상이 되었고, 이때 섞은 횟수는 2회입니다.


## 내 풀이 (시간초과)

```python
  1 def solution(scoville, k):
  2     mix_cnt = 0
  3     while min(scoville) < k:
  4         scoville.sort()
  5         try:
  6             scoville.append(scoville.pop(0) + (scoville.pop(0) * 2))
  7         except IndexError:
  8             return -1
  9         mix_cnt += 1
 10
 11     return mix_cnt
```

모든 스코빌 지수가 k 이상이 되려면, 가장 작은 스코빌 지수가 k 이상이면 된다.

(2) 우선 음식을 섞은 횟수를 기록할 변수를 0으로 초기화해준다.

(3) 그러므로, 가장 작은 스코빌 지수가 k보다 작다면, loop을 계속 돌린다.

(4) 가장 작은 스코빌 지수부터 차례대로 정렬을 해준다.

(6) 가장 작은 스코빌 지수와 그 다음으로 작은 스코빌 지수를 뽑아 계산을 한 후, 다시 scoville 리스트에 넣어준다.

(8) 만약 남아있는 요소가 없어서 인덱스 에러가 난다면,

이는 모든 음식의 스코빌 지수를 k 이상으로 만들 수 없는 경우이므로 -1을 리턴한다.

(9) 에러가 나지 않고 무사히 계산을 끝냈다면 mix_cnt를 한 개 증가시켜준다.

<br/>

로직에는 문제가 없으나, 효율성(아마도 속도) 테스트를 통과하지 못했다.

4번 라인에서 매번 loop을 돌때마다 리스트를 정렬하는 작업이 들어가므로,

리스트의 크기가 매우 클 경우 정렬에 드는 비용을 감당하지 못하는 것 같다.


## 내 풀이 (정답)

```python
  1 import heapq
  2
  3
  4 def solution(scoville, k):
  5     heap = []
  6     for num in scoville:
  7         heapq.heappush(heap, num)
  8
  9     mix_cnt = 0
 10     while heap[0] < k:
 11         try:
 12             heapq.heappush(heap, heapq.heappop(heap) + (heapq.heappop(heap) * 2))
 13         except IndexError:
 14             return -1
 15         mix_cnt += 1
 16
 17     return mix_cnt
```

heapq를 사용했다.

heapq는 일반적인 리스트와 다르게, 가지고 있는 요소를 push, pop 할때마다 자동으로 정렬해주는 녀석이다.

따라서, 앞서 문제가 되었던 정렬 비용을 감소시킴으로써 효율성 이슈를 해결했다.

(5) heapq로 사용할 리스트를 초기화한다.

(6~7) 기존 리스트에 있던 요소들을 heapq에 넣어준다. heappush 라는 메소드를 이용한다.

맨 앞의 요소를 가져올때 heappop 메소드를 이용한다는 사실을 제외하고 나머지는 똑같다.



## 분석

예전에 회사 동기 A랑 sort를 활용한 어떤 문제를 풀었을때,

나는 그냥 어떻게든 정답을 맞추고 끝냈었다.

하지만 A는 불현듯 뭔가에 꽂혔는지, "sort보다 더 빠른 방법이 없을까?" 하는 고민을 했었다.

<br/>

A와 나는 직접 소트 기능을 구현해서 이것저것 시도했지만,

파이썬에 내장된 sort가 생각보다 빨라서 좀처럼 따라잡지 못했었다.

나는 이내 포기하고 푼 문제를 정리하고 있었고, A는 계속 시도했다.

<br/>

그리고 퇴근시간쯤이 되어서야 heapq를 활용해 드디어 sort의 속도를 따라잡는데 성공했었고,

A는 나에게 뭔가 설명해줬는데 마음이 급해서 그랬는지, 별로 이해하고자 하는 의지가 없어서 그랬는지,

그저 퇴근하는데 급급해서 "아아... 뭐 그냥 그런게 있거나, A가 뭔가 착각한 것" 이라고 생각하고 말았다.

<br/>

그런데 이번 문제를 풀며 이것저것 서치해보니, 그때 A가 사용했던 heapq라는 녀석이 튀어나왔다.

아마 그때 대수롭게 넘기지 않고 한 번 더 물어봤다면, 이번 문제는 훨씬 빠르게 해결할 수 있었을 것이다.

항상 다른 사람의 말을 경청하고, 건방진(?) 자세를 고치는 것 또한 개발자의 중요한 덕목인 것 같다.