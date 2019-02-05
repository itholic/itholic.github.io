---
title: "[kata][python] 프로그래머스 - 쇠막대기"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 쇠막대기

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42585" target="_blank">프로그래머스 - 쇠막대기 </a>

## 문제

여러 개의 쇠막대기를 레이저로 절단하려고 합니다.

효율적인 작업을 위해서 쇠막대기를 아래에서 위로 겹쳐 놓고,

레이저를 위에서 수직으로 발사하여 쇠막대기들을 자릅니다.

쇠막대기와 레이저의 배치는 다음 조건을 만족합니다.

```
쇠막대기는 자신보다 긴 쇠막대기 위에만 놓일 수 있습니다.
쇠막대기를 다른 쇠막대기 위에 놓는 경우 완전히 포함되도록 놓되, 끝점은 겹치지 않도록 놓습니다.
각 쇠막대기를 자르는 레이저는 적어도 하나 존재합니다.
레이저는 어떤 쇠막대기의 양 끝점과도 겹치지 않습니다.
```

아래 그림은 위 조건을 만족하는 예를 보여줍니다.

수평으로 그려진 굵은 실선은 쇠막대기이고, 점은 레이저의 위치,

수직으로 그려진 점선 화살표는 레이저의 발사 방향입니다.


![example](/assets/images/2019/02/04/kata-iron-stick/example.png)


이러한 레이저와 쇠막대기의 배치는 다음과 같이 괄호를 이용하여 왼쪽부터 순서대로 표현할 수 있습니다.

```
(a) 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 '()'으로 표현합니다.
또한 모든 '()'는 반드시 레이저를 표현합니다.

(b) 쇠막대기의 왼쪽 끝은 여는 괄호 '('로, 오른쪽 끝은 닫힌 괄호 ')'로 표현됩니다.
위 예의 괄호 표현은 그림 위에 주어져 있습니다.
쇠막대기는 레이저에 의해 몇 개의 조각으로 잘리는데,
위 예에서 가장 위에 있는 두 개의 쇠막대기는 각각 3개와 2개의 조각으로 잘리고,
이와 같은 방식으로 주어진 쇠막대기들은 총 17개의 조각으로 잘립니다.
```

쇠막대기와 레이저의 배치를 표현한 문자열 arrangement가 매개변수로 주어질 때,

잘린 쇠막대기 조각의 총 개수를 return 하도록 solution 함수를 작성해주세요.


### 제한사항

arrangement의 길이는 최대 100,000입니다.

arrangement의 여는 괄호와 닫는 괄호는 항상 쌍을 이룹니다.

### 입출력 예

```
arrangement: "()(((()())(())()))(())"
return: 17
```


## 내 풀이

```python
  1 def solution (arrangement):
  2     answer = 0
  3     num_stick = 0
  4     last = "open"
  5
  6     for token in arrangement:
  7         if token == "(":
  8             num_stick += 1
  9             last = "open"
 10         else:
 11             if last == "open":
 12                 # laser
 13                 num_stick -= 1
 14                 answer += num_stick
 15                 last = "close"
 16             else:
 17                 # end of stick
 18                 num_stick -= 1
 19                 answer += 1
 20
 21     return answer
```

(6) 입력받은 괄호를 하나씩 순회합니다.

(7~9) 열린 괄호일 경우 막대기 갯수를 하나 증가시키고, 마지막 요소(last)를 "open" 으로 표시합니다.

(10~15) 닫힌 괄호인데 last가 "open"일 경우, 이는 괄호가 열렸다가 바로 닫힌 레이저를 의미합니다.

따라서 앞에서 추가한 막대기 갯수를 하나 감소시키고, 결과 값에 현재 가지고있는 막대기 갯수만큼을 추가합니다.

(16~17) 닫힌 괄호인데 last가 "open"이 아닐 경우, 이는 막대기의 끝을 의미합니다.

단순히 막대기 갯수를 하나 없애고 끝내면 안됩니다. 막대기의 마지막 꼬리 부분 1을 추가해주어야 합니다.




## 분석

풀고나서 코드를 다시보니,

last라는 변수에 "open" 이나 "close" 대신 그냥 순회중인 token을 그대로 넣는것이 더 깔끔했을 것 같다.

그리고 num_stick과 같은 정수형 변수에 숫자를 1씩 추가하면서 할 수도 있겠지만,

list를 사용해서 "(" 모양일 경우 하나씩 넣어주고, 그 길이를 결과값에 더해나가는 식이 더 세련되었을 것 같다.

예를들면 이렇게.

```python
def solution (arrangement):
    token_stack = []
    answer = 0

    for token in arrangement:
        if token == "(":
            token_stack.append(token)
            last = token
        else:
            if last == "(":
                token_stack.pop()
                answer += len(token_stack)
                last = token
            else:
                token_stack.pop()
                answer += 1

    return answer
```

그리고 문제의 카테고리가 '스택/큐'인 것을 봐서는 아마도 이게 더 출제자(?)의 의도에 맞는 답일지도 모르겠다.
