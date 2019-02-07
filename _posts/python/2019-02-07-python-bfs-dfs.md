---
title: "[python] 파이썬으로 bfs, dfs 구현해보기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# BFS, DFS

우선 BFS, DFS가 뭔지부터 알아보자.



## BFS, DFS 개념

다음과 같은 그래프가 있다고하자. (PPT로 그린거라 좀 허접해도 양해바람)



![](/assets/images/2019/02/07/python-graph/graph.png)



A부터 시작해서 모든 노드를 순회하는 방법은 다음과 같이 크게 두가지가 있을 것이다.

그림과 비교하면서 눈으로 잘 따라가보자.



1. A - B - C - H - D - I - J - M - E - G - K - F - L

2. A - B- C - D - E - F - G - H - I - J - K - L - M


<br/>

1번 방식은 한 단계씩 나아가면서 해당 노드와 같은 레벨에 있는 노드들(즉, 형제 노드들)을 먼저 순회하는 방식이다.

이러한 방식을 Breath First Search (너비 우선 탐색, BFS) 라고 한다. 

<br/>

2번 방식은 한 노드의 자식을 타고 끝까지 순회한 다음에, 다시 돌아와서 다른 형제의 자식을 타고 내려가며 순회하는 방식이다.

방문 순서와 그림을 대조해서 보면 이해가 갈것이다.

이러한 방식은 Depth First Search (깊이 우선 탐색, DFS) 라고 한다.

<br/>

## 파이썬으로 구현해보기

그래프를 다시 가져와보자.

![](/assets/images/2019/02/07/python-graph/graph.png)

파이썬에서 BFS, DFS를 구현하기 위해서는 우선 그래프를 코드로 표현해야한다.

한 노드를 중심으로 연결관계가 있는 노드를 모두 표현해주면 될 것이다.

여러가지 방법이 있겠지만, 딕셔너리와 리스트를 사용해 표현해보자.

```python
graph = {
    'A': ['B'],
    'B': ['A', 'C', 'H'],
    'C': ['B', 'D', 'G'],
    'D': ['C', 'E'],
    'E': ['D', 'F'],
    'F': ['E'],
    'G': ['C'],
    'H': ['B', 'I', 'J', 'M'],
    'I': ['H'],
    'J': ['H', 'K'],
    'K': ['J', 'L'],
    'L': ['K'],
    'M': ['H']
}
```


그림이랑 코드를 잘 비교해서 보면 대충 모양새가 이해될것이다.

<br/>

## Python - BFS

우선 BFS를 먼저 구현해보자.

```python
  1 def bfs(graph, start_node):
  2     visit = list()
  3     queue = list()
  4
  5     queue.append(start_node)
  6
  7     while queue:
  8         node = queue.pop(0)
  9         if node not in visit:
 10             visit.append(node)
 11             queue.extend(graph[node])
 12
 13     return visit
```

앞서 만든 그래프와 시작 노드를 받아서 BFS 방식으로 그래프를 순회하는 함수이다.

(2~3) 방문했던 노드 목록을 차례대로 저장할 리스트와, 다음으로 방문할 노드의 목록을 차례대로 저장할 리스트(큐)를 만들어주자.

(5) 우선 맨 처음에는 당연히 시작 노드를 큐에 넣어준다.

(7) 큐의 목록이 바닥날때까지(더 이상 방문할 노드가 없을 때까지) loop를 돌려준다.

(8) 큐의 맨 앞에있는 노드를 꺼내온다.

(9) 해당 노드가 아직 방문 리스트에 없다면, 

(10) 방문 리스트에 추가해주고,

(11) 해당 노드의 자식 노드들을 큐에 추가해준다.

<br/>

자식 노드들을 큐에 추가하면서 큐에 먼저 추가됐던 노드부터 순차적으로 방문하게되면 결국엔 BFS형태로 순회하게 된다.

코드는 별로 어렵지 않지만, 처음 보면 직관적으로 와닿지는 않을것이다.

맨 아래쪽에 전체 코드를 첨부했으니, 

코드를 복사해서 while문 안에 visit와 queue를 출력하며 한 단계씩 과정을 살펴보면 보다 쉽게 이해가 될 것이다.

<br/>

## Python - DFS 

이번엔 DFS를 구현해보자.

코드 기준으로 봤을때 DFS는 BFS와 거의 똑같고, queue대신 stack을 사용한다는 점만 다르다.

```python
  1 def dfs(graph, start_node):
  2     visit = list()
  3     stack = list()
  4
  5     stack.append(start_node)
  6
  7     while stack:
  8         node = stack.pop()
  9         if node not in visit:
 10             visit.append(node)
 11             stack.extend(graph[node])
 12
 13     return visit
```

queue의 변수명이 stack으로 바뀌었고, 8번 라인에서 pop(0) 을 하던 부분이 pop() 으로 바뀌었다.

리스트에서 pop()을 하게되면 맨 마지막에 넣었던 아이템을 가져오게 되므로 stack과 동일하게 동작하게 된다.

반대로 pop(0)을 하게되면 맨 앞에있는 요소를 가져오므로 queue와 동일하게 동작했던 것이다. 

<br/>

## 전체 코드

마지막으로 공부하면서 정리한 전체 코드를 공유한다.

나도 100% 이해한채로 구현했다고 하기엔 어려워서,

혹시 개선할 부분이 있거나 잘못 구현된 부분이 있다면 꼭 댓글을 달아줬으면 좋겠다!

```python
  1 def bfs(graph, start_node):
  2     visit = list()
  3     queue = list()
  4
  5     queue.append(start_node)
  6
  7     while queue:
  8         node = queue.pop(0)
  9         if node not in visit:
 10             visit.append(node)
 11             queue.extend(graph[node])
 12
 13     return visit
 14
 15
 16 def dfs(graph, start_node):
 17     visit = list()
 18     stack = list()
 19
 20     stack.append(start_node)
 21
 22     while stack:
 23         node = stack.pop()
 24         if node not in visit:
 25             visit.append(node)
 26             stack.extend(graph[node])
 27
 28     return visit
 29
 30
 31 if __name__ == "__main__":
 32     graph = {
 33         'A': ['B'],
 34         'B': ['A', 'C', 'H'],
 35         'C': ['B', 'D', 'G'],
 36         'D': ['C', 'E'],
 37         'E': ['D', 'F'],
 38         'F': ['E'],
 39         'G': ['C'],
 40         'H': ['B', 'I', 'J', 'M'],
 41         'I': ['H'],
 42         'J': ['H', 'K'],
 43         'K': ['J', 'L'],
 44         'L': ['K'],
 45         'M': ['H']
 46     }
 47
 48     print(bfs(graph, 'A'))
 49     print(dfs(graph, 'A'))
```



나 또한 이제 공부를 막 시작한지라 많이 부족하지만, 대강의 개념을 잡는 정도로 누군가에게 도움이 되었으면 좋겠다.
