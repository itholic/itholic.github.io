---
title: "[kata][python] 프로그래머스 - 완주하지 못한 선수"
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

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42576" target="_blank">프로그래머스 - 완주하지 못한 선수</a>

## 문제

수많은 마라톤 선수들이 마라톤에 참여하였습니다.

단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와

완주한 선수들의 이름이 담긴 배열 completion이 주어질 때,

완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.

### 제한사항

completion의 길이는 participant의 길이보다 1 작습니다.

참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.

참가자 중에는 동명이인이 있을 수 있습니다.

### 입출력 예

```
participant: [mislav, stanko, mislav, ana]
completion: [stanko, ana, mislav]
return: "mislav"
```



## 내 풀이

```python
  1 def solution(participant, completion):
  2     completion.append("z" * 20)
  3
  4     for p_name, c_name in zip(sorted(participant), sorted(completion)):
  5         if p_name != c_name:
  6             return(p_name)
```

단 한명만 완주하지 못한다는 조건이 있으므로,

완주자 배열은 항상 참여자 배열보다 1명이 부족하다.

(2) 부족한 한명의 이름을 임의로 채워넣고,

(4) 참여자와 완주자 리스트를 정렬해 비교하다가

(5) 이름이 다른경우 리턴했다.

이 때 임의로 채워넣는 선수의 이름은 항상 배열의 맨 끝으로 가도록 "z" 20개로 설정했다.

임의로 채워넣은 선수의 이름이 배열의 맨 끝이 아닌 중간으로 오게되면,

리스트 정렬시 해당 선수의 이름이 있는 부분에서 잘못 리턴될 확률이 아주 높기 때문이다.


## 다른 사람 풀이

```python
import collections

def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
```

Counter를 사용해 간단히 해결했다.



## 분석

파이썬을 1~2년가량 써오면서 나름 대부분의 기능을 활용했다고 생각했는데,

최근들어 내가 알고있는 기능은 빙산의 일각일 뿐이라는걸 깨달았다.

여러모로 시간을 절약하고 생산성을 높이기 위해 보다 적극적으로 여러 모듈을 공부하고 실무에 적용해봐야겠다.

collections 모듈에 있는 namedtuple, deque같은 기능도 한 번 공부해보고 여러방향으로 적용하도록 시도해야겠다.