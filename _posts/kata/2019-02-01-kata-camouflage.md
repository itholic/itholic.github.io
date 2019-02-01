---
title: "[kata][python] 프로그래머스 - 위장"
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

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42578" target="_blank">프로그래머스 - 위장 </a>

## 문제

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.


### 제한사항

clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.

스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.

같은 이름을 가진 의상은 존재하지 않습니다.

clothes의 모든 원소는 문자열로 이루어져 있습니다.

모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.

스파이는 하루에 최소 한 개의 의상은 입습니다.

### 입출력 예

```
clothes: [[yellow_hat, headgear], [blue_sunglasses, eyewear], [green_turban, headgear]]
return: 5
```

### 입출력 예 설명

headgear에 해당하는 의상이 yellow_hat, green_turban이고,

eyewear에 해당하는 의상이 blue_sunglasses이므로,

아래와 같이 5개의 조합이 가능합니다.

```
1. yellow_hat
2. blue_sunglasses
3. green_turban
4. yellow_hat + blue_sunglasses
5. green_turban + blue_sunglasses
```

## 내 풀이

```python
  1 from collections import Counter
  2
  3 def solution(clothes):
  4     counter_each_category = Counter([cat for _, cat in clothes])
  5     all_possible = 1
  6
  7     for key in counter_each_category:
  8         all_possible *= (counter_each_category[key] + 1)
  9
 10     return all_possible - 1
```

각 아이템에는 해당하는 카테고리가 있고,

카테고리별로 아이템을 한 개씩 조합해야 하는 문제이다.

단순히 생각하면 다음과같이 각 카테고리별 아이템 갯수를 구해서 다 곱하면 될 것 같다.

```(모자의갯수) * (바지의갯수) * (안경의갯수)```

하지만 이렇게하면 각 카테고리의 아이템이 "하나씩은 반드시 포함"되는 경우만 계산된다.

예를들어 모자는 쓰지 않고 바지만 입는다거나 하는 경우는 고려되지 않는다.

모자랑 안경만 쓰고 바지는 입지 않는 경우도 고려되지 않는다.

하지만 우리는 이러한 경우도 모두 고려해야한다.

따라서 각 카테고리별로 다음과 같이 "해당 카테고리의 아이템을 장착하지 않는 경우" 한개를 더 추가해서 계산해야한다.

```(모자의갯수 + 1) * (바지의갯수 + 1) * (안경의갯수 + 1)```

이렇게하면 특정 카테고리가 제외되는 경우까지 모두 고려된다.

하지만 여기서 끝내면 안된다.

스파이는 반드시 한 개의 아이템은 장착해야 하므로,

어떤 아이템도 장착하지 않는 한 개의 경우는 결과에서 빼줘야한다.

즉, 최종 계산은 다음과 같은 형태가 된다.

```(모자의갯수 + 1) * (바지의갯수 + 1) * (안경의갯수 + 1) - 1```

<br/>

이제 코드를 보자.

(4) 일단 각 카테고리(모자, 안경,  상의 등)별로 아이템의 갯수를 구한다.

(7~8) 각 카테고리별로 가지고있는 아이템의 수에 1을 더해서 다 곱해준다.

(10) 모든 경우의 수에서 아무런 아이템도 착용하지 않는 경우 하나를 빼고 리턴해준다


## 다른 사람 풀이

```python
  1 from collections import defaultdict
  2 from functools import reduce
  3 from operator import mul
  4
  5 def solution(clothes):
  6     num_clothes_kind = defaultdict(int)
  7     for name, kind in clothes:
  8         num_clothes_kind[kind] += 1
  9
 10     tmp = [ num + 1 for num in num_clothes_kind.values() ]
 11     answer = reduce(mul, tmp)
 12     answer = answer -1
 13     return answer
```

로직은 똑같다.

다만 defaultdict, reduce, mul 등 다양한 모듈을 활용했다.

Counter대신 defaultdict에 카테고리 이름마다 1씩 더해주는 방식으로 카테고리 갯수를 구했다.

## 분석

reduce, mul과 내 코드를 조합하면 조금 더 간결한 코드를 짤 수 있을 것 같았다.

```python
  1 from collections import Counter
  2 from functools import reduce
  3 from operator import mul
  4
  5 def solution(clothes):
  6     return reduce(mul, [cnt + 1 for cnt in Counter([cat for _, cat in clothes]).values()]) - 1
```

큰 의미는 없지만 한 번 줄여봤다.

여러 모듈을 적절히 활용하면 복잡한 문제를 단순하고 깔끔하게 표현할 수 있는 것 같다.

무조건 코드를 줄인다고 좋은건 아니지만,

여러 모듈을 사용해보면 확실히 실무에서 유연한 사고를 하는데 꽤나 도움이 되는 것 같다.
