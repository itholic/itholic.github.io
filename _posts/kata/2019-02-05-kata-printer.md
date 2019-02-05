---
title: "[kata][python] 프로그래머스 - 프린터"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 프린터

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42587" target="_blank">프로그래머스 - 프린터 </a>

## 문제

일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다.

그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다.

이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다.

이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

```
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.

2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면,
   J를 대기목록의 가장 마지막에 넣습니다.

3. 그렇지 않으면 J를 인쇄합니다.
```

예를 들어,

4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고, 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다.

위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와

내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때,

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.



### 제한사항

a현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.

인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.

location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며,

대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.


### 입출력 예

```
#1
priorities: [2, 1, 3, 2]
location: 2
return: 1

#2
priorities: [1, 1, 9, 1, 1, 1]
location: 0
return: 5
```

### 입출력 예 설명

예제 #1

문제에 나온 예와 같습니다.

예제 #2

6개의 문서(A, B, C, D, E, F)가 인쇄 대기목록에 있고 중요도가 1 1 9 1 1 1 이므로 C D E F A B 순으로 인쇄합니다.

## 내 풀이

```python
  1 def solution(priorities, location):
  2     pi_list = [(p, i) for i, p in enumerate(priorities)]
  3     waiting_q = []
  4
  5     while pi_list:
  6         pi = pi_list.pop(0)
  7         priority = pi[0]
  8         p_list = [priority for priority, idx in pi_list]
  9         if p_list:
 10             max_p = max(p_list)
 11
 12         if priority >= max_p:
 13             waiting_q.append(pi)
 14         else:
 15             pi_list.append(pi)
 16
 17     for i, item in enumerate(waiting_q):
 18         if item[1] == location:
 19             return i + 1
```

이 문제의 관건은 인쇄 목록과 각 목록의 인덱스를 함께 기억하는 것이라고 생각했다.

(2) 이를 위해 우선 인자로 받은 인쇄 목록과 그 인덱스번호를 함께 튜플로 만들어서 리스트(pi_list)를 생성했다.

예를들어 [1, 2, 3, 4, 5, 4, 3, 5] 라는 인쇄목록을 받았다면, 이 리스트의 형태는 다음과 같이 될 것이다.

[(1, 0), (2, 1), (3, 2), (4, 3), (5, 4), (4, 5), (3, 6), (5, 7)]

(3) 최종 출력될 인쇄물들을 순서대로 집어넣을 queue(waiting_q)를 만들었다.

(5) pi_list에 있는 모든 목록을 waiting_q에 넣을때까지 반복을 계속한다.

(6~7) pi_list의 첫번째 아이템을 뽑아와서 priority를 구한다.

(8) pi_list에서 priority만 뽑아와서 list를 만든다.

위에서 pi_list의 첫번째 목록을 pop 했으므로 첫번째 목록을 제외한 나머지 목록으로 리스트가 만들어질 것이다.

(9~10) 최고 우선순위 값을 구한다

(12~13) 첫 번째 아이템의 우선순위가 전체 우선순위보다 크거나 같다면, waiting_q에 바로 넣어준다.

(14~15) 그렇지 않다면, 처음에 뽑았던 아이템을 pi_list의 맨 뒤로 추가해준다.

(17~19) 최종 완성된 waiting_q에서 location과 일치하는 index를 가진 아이템을 찾는다.

index는 0부터 시작되므로, 문서가 '몇 번째로' 출력됐는지 알기 위해 1을 더해주어 리턴한다.

## 다른사람 풀이

```python
def solution(p, l):
    ans = 0
    m = max(p)
    while True:
        v = p.pop(0)
        if m == v:
            ans += 1
            if l == 0:
                break
            else:
                l -= 1
            m = max(p)
        else:
            p.append(v)
            if l == 0:
                l = len(p)-1
            else:
                l -= 1
    return ans
```

받은 인자 중에 priorities를 바꿀 생각만 했었는데,

이 경우는 location값을 하나씩 빼고, ans 값을 추가해가면서 답에 접근하는 방식을 사용했다.

내가 했던 방식처럼 추가적인 list를 선언하지 않고도 깔끔하게 문제 해결이 가능하다.

전체적인 로직은 이해가 되지만 모든 라인이 직관적으로 와닿지는 않아서 line by line 분석은 시간이 좀 걸릴 것 같다.

생각보다 이런 방식으로 푼 사람들이 꽤 되는것을 보고 아직 내공이 많이 부족함을 다시 한 번 깨달았다


## 분석

문제만 봤을땐 엄청 쉬울줄알았는데 막상 풀다보니 테스트케이스가 절반도 통과되지 않는 상황이 발생했다.

처음에도 튜플에 인덱스 번호와 우선순위를 저장하는 방법을 생각 했었지만,

분명 이것보다 훨씬 간결하고 괜찮은 방법이 있을것같다는 생각이 들어서 이것저것 계속 시도했었다.

전달받은 인자 중 한개만 가지고 풀려고 계속 머리를 싸맸었는데,

주어진 모든 데이터 가능한 여러 방향으로 적용해보는 방법에 대해 많은 고민이 필요할 것 같다.