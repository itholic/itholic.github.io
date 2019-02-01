---
title: "[kata][python] 프로그래머스 - 베스트앨범"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 위장

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42579" target="_blank">프로그래머스 - 베스트앨범 </a>

## 문제

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다.

노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

노래의 장르를 나타내는 문자열 배열 genres와

노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때,

베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.


### 제한사항

genres[i]는 고유번호가 i인 노래의 장르입니다.

plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.

genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.

장르 종류는 100개 미만입니다.

장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.

모든 장르는 재생된 횟수가 다릅니다.

### 입출력 예

```
genres: ["classic", "pop", "classic", "classic", "pop"]
plays: [500, 600, 150, 800, 2500]
return: [4, 1, 3, 0]
```

### 입출력 예 설명

classic 장르는 1,450회 재생되었으며, classic 노래는 다음과 같습니다.

```
고유 번호 3: 800회 재생
고유 번호 0: 500회 재생
고유 번호 2: 150회 재생
```

pop 장르는 3,100회 재생되었으며, pop 노래는 다음과 같습니다.

```
고유 번호 4: 2,500회 재생
고유 번호 1: 600회 재생
```

따라서 pop 장르의 [4, 1]번 노래를 먼저, classic 장르의 [3, 0]번 노래를 그다음에 수록합니다.

## 내 풀이

```python
  1 from collections import defaultdict
  2 from operator import itemgetter
  3
  4 def solution(genres, plays):
  5     genre_play_dict = defaultdict(lambda: 0)
  6     for genre, play in zip(genres, plays):
  7         genre_play_dict[genre] += play
  8
  9     genre_rank = [genre for genre, play in sorted(genre_play_dict.items(), key=itemgetter(1), reverse=True)]
 10
 11     final_dict = defaultdict(lambda: [])
 12     for i, genre_play_tuple in enumerate(zip(genres, plays)):
 13         final_dict[genre_play_tuple[0]].append((genre_play_tuple[1], i))
 14
 15     answer = []
 16     for genre in genre_rank:
 17         one_genre_list = sorted(final_dict[genre], key=itemgetter(0), reverse=True)
 18         if len(one_genre_list) > 1:
 19             answer.append(one_genre_list[0][1])
 20             answer.append(one_genre_list[1][1])
 21         else:
 22             answer.append(one_genre_list[0][1])
 23
 24     return answer
```

(5~9) 우선 플레이 횟수의 합이 가장 큰 장르를 순서대로 집어넣은 리스트(genre_rank)를 만들었다.

(11~13) 다음과 같이 장르명을 key로 가지며, 값으로는 각 노래의 플레이 횟수와 고유번호를 리스트로 저장하는 딕셔너리(final_dict)를 만들었다.

```{"classic": [(500, 0), (150, 2), (800, 3)], "pop": [(600, 1), (2500, 4)]```

(15~22) 앞서 만든 genre_rank를 차례대로 순회하며, 플레이 횟수가 가장 많은 장르부터 해당 장르에서 가장 많이 플레이된 2개의 곡을 answer에 차례로 넣어주었다.(곡이 2개 미만이면 1개만 넣어준다)



## 다른 사람 풀이

```python
  1 from collections import defaultdict
  2
  3 def solution(genres, plays):
  4     play_count_by_genre = defaultdict(int)
  5     songs_in_genre = defaultdict(list)
  6
  7     for song_id, genre, play in zip(counter(), genres, plays):
  8         play_count_by_genre[genre] += play
  9         songs_in_genre[genre].append((-play, song_id))
 10
 11     genre_in_order = sorted(play_count_by_genre.keys(), key=lambda g:play_count_by_genre[g], reverse=True)
 12
 13     answer = list()
 14     for genre in genre_in_order:
 15         print(genre)
 16         answer.extend([ song_id for minus_play, song_id in sorted(songs_in_genre[genre])[:2]])
 17     return answer
 18
 19 def counter():
 20     i = 0
 21     while True:
 22         yield i
 23         i += 1

```

다른 사람들의 풀이를 보면 로직은 거의 같다.

(7~9) 장르를 key로 하고, 플레이 횟수와 고유번호를 튜플로 리스트에 추가한다는 부분은 대부분 비슷한 생각을 한 것 같다.

이 코드에서 인상적인건 고유번호를 생성해내는 부분이었는데,

counter() 라는 제너레이터를 만들어서 해결한것이 인상적이었다.

7번째 라인에 보면 zip을 만들때 counter() 를 사용해 만들었는데,

이렇게하면 zip에 들어간 나머지 인자의 최소길이만큼 자동으로 번호가 생성된다는 것을 알게되었다.



## 분석

generator외에도 class나 namedtuple을 사용해 해결한 케이스도 있었는데,

class를 만들때도 클래스명이 제각각이며 스타일도 다 달랐다.

제네레이터를 공부는 했지만 실제로 어떻게 적용할지 막막했는데 활용예시를보니 조금은 알 것도 같다.

역시 문제를 풀때마다 내가 공부했던 파이썬은 정말 빙산의 일각의 일각이라는 생각이든다.

절차형으로 쭉 기술하는 방법도 나쁘진 않지만, 여러 객체를 고루고루 사용하면서 생각의 폭을 넓혀야겠다.