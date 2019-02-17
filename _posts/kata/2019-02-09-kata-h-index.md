---
title: "[kata][python] 프로그래머스 - H-Index"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 완주하지 못한 선수

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42747" target="_blank">프로그래머스 - H-Index</a>

## 문제

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다.

어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다.

위키백과[1](https://programmers.co.kr/learn/courses/30/lessons/42747?language=python3#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`가 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때,

이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

##### 입출력 예

| citations       | return |
| --------------- | ------ |
| [3, 0, 6, 1, 5] | 3      |

##### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

## 내 풀이

```python
  1 def solution(citations):
  2     for h in range(max(citations), 0, -1):
  3         over_h = 0
  4         for citation in citations:
  5             if citation >= h:
  6                 over_h += 1
  7             if over_h == h:
  8                 return h
```

(2) 논문 인용 리스트(citations)에서 가장 많이 인용된 논문의 갯수부터 0까지 iteration을 돌려준다.

큰 숫자부터 내려가면서 iteration하는 이유는, H-INDEX는 H번 이상 인용된 논문이 H개 이상일 때, H의 최대 값으로 봐야하기 때문이다.

<br/>

예를들어 `[4, 4, 4, 4, 5, 5, 5, 5, 5, 6, 6, 6, 6, 6, 6]` 이라는 리스트가 있을때,

우선 **"h번 이상 인용된 논문이 h편 이상"** 에 부합하는 경우를 찾아보면

1. 4회 이상 인용된 논문이 4개 이상 (15개), 
2. 5회 이상 인용된 논문이 5개 이상 (11개),
3. 6회 이상 인용된 논문이 6개 이상이다 (6개).

이렇게만 보면 H-INDEX가 세 개나 나온 것 같지만, 그렇지않다.

**"나머지 논문이 h번 이하 인용되었다면"** 이라는 조건까지 따져보면,

1. 4회 이상 인용된 논문이 4개 이상, 나머지 논문은 15번 인용
2. 5회 이상 인용된 논문이 5개 이상, 나머지 논문은 11번 인용
3. 4회 이상 인용된 논문이 6개 이상, 나머지 논문은 6번 인용

문제의 조건에 완벽히 부합하는 H-INDEX는 6 하나밖에 없다는 사실을 알 수 있다.

다시 말해, **"h번 이상 인용된 논문이 h편 이상이되는, h의 최대값"**을 구하는 것과 같다.

<br/>

즉, 높은 인용수부터 내려오면서 iteration을 돌다가, 가장 처음으로 발견된 h값을 리턴해주면 된다.

사실 이 부분이 문제에 자세하게 명시되어있지 않아서 혼동이 왔을수 있다. 나도 링크 걸려있는 위키를 보고 정확히 이해했다.

(3) 인용수가 h 이상인 논문이 몇개인지 카운팅하기위해 `over_h` 라는 변수를 선언했다.

(4~8) 논문 인용수 리스트를 하나씩 돌면서, 인용수가 h보다 큰 경우 `over_h` 의 카운트를 하나씩 증가하고, 그 수가 h의 값과 같아지는 순간, 해당 h를 리턴해주면 된다.

<br/>



## 분석

문제를 다 풀었는데, 9번 테스트 케이스 딱 한 개가 통과되지 않아서 시간을 좀 잡아먹었다.

원인이 뭐였냐면,

처음에 짰던 코드는 iteration을 돌 때 `range(max(citations), min(citations) - 1, -1)` 의 조건으로 돌렸었다.

즉, 인용 리스트에 있는 가장 큰 수부터 가장 작은 수까지 내려가면서 iteration을 했는데,

인용 리스트에 있는 가장 큰 수부터 가장 작은 수까지가 아니라, 0까지 iteration을 돌렸어야했다.

예제에 나온 테스트케이스에는 항상 0이 포함되어있어서 실수를했다.

혹시나 나처럼 9번 테스트 케이스가 통과되지 않는 사람이 있다면,

 `citations = [10, 50, 100]` 으로 테스트를 해 보면 무슨말인지 알 것이다.

참고로 이 경우 H-INDEX는 3이 나와야한다.

일단 **"h번 이상 인용된 논문이 h편 이상"** 이라는 부분에서, 내가 예제에 들었던 것처럼 조건에 만족하는 h가 두 개 이상이면 어떻게 처리해야 할지 확신이 서지 않았다. 

한참 삽질을 하고나서

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 **"나머지 논문이 h번 이하 인용되었다면"** `h`가 이 과학자의 H-Index입니다.