---
title: "[kata][python] 프로그래머스 - 소수 찾기"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 소수 찾기

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/42839" target="_blank">프로그래머스 - 소수 찾기</a>

## 문제

한자리 숫자가 적힌 종이 조각이 흩어져있습니다.

흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때,

종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

### 제한사항

numbers는 길이 1 이상 7 이하인 문자열입니다.

numbers는 0~9까지 숫자만으로 이루어져 있습니다.

013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

### 입출력 예

|numbers	|return|
|---|---|
|17|	3|
|011|	2|


### 입출력 예 설명

예제 #1

```
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.
```

예제 #2

```
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

* 11과 011은 같은 숫자로 취급합니다.
```

## 내 풀이


```python
  1 from itertools import permutations
  2 import math
  3
  4 limit = 9999999
  5 eratos = [1] * (2 * limit + 1)
  6 eratos[0] = 0
  7 eratos[1] = 1
  8
  9 for i in range(2, int(math.sqrt(len(eratos)))):
 10     if eratos[i]:
 11         for j in range(i + i, len(eratos), i):
 12             eratos[j] = 0
 13
 14 def solution(numbers):
 15     permutation_set = set([int("".join(item)) for i in range(7) for item in set(permutations(list(numbers), i + 1)    )])
 16     prime_list = [eratos[num] for num in permutation_set if num != 0 and num != 1]
 17
 18     return sum(prime_list)
```

에라토스테네스의 체를 사용해 풀었다.

쉽게 말해 제한된 범위(9999999)내에 있는 소수를 미리 다 구해놓고, 나중에 꺼내오기만 하는 것이다.

더 자세한 내용은 <a href="https://itholic.github.io/kata-bertrands-postulate/" target="_blank">전에 풀었던 문제</a>에 설명을 적어놨으니 참고하면 될 것 같다.

(4~12) 에라토스테네스의 체를 선언한다 (제한된 범위내에 있는 소수를 미리 다 구해놓는 것이다)

(15) permutations를 이용해 입력받은 숫자로 만들 수 있는 모든 순열을 구하고, 중복되는건 제거한다.

(16) 미리 만들어놓은 에라토스테네스의 체를 통해 소수인 경우 1, 아닌경우 0을 prime_list에 저장한다.

(18) prime_list의 합을 구해 출력한다 (소수일 경우에만 1이므로, 리스트의 값을 다 더하면 전체 소수의 개수이다)



## 분석

예전에 문제를 풀때 공부한 개념들이 도움이되어 매우 쉽고 빠르게 풀 수 있었다.

(물론 최선의 성능을 내는 코드냐 하는 것은 또 다른 문제이지만...)

<br/>

최근에 공부했던 itertools의 permutation을 통해 순열을 구했고,

예전에 공부했던 에라토스테네스의 체를 통해 소수를 걸러낼 리스트를 만들었다.

<br/>

문제 자체가 그렇게 난이도가 높은 것은 아니었지만,

아마 이러한 선행 공부들이 되어있지 않았다면 이보다는 시간이 훨씬 오래 걸렸을것이다.

풀고 나서도 예전처럼 소수를 계산하는 과정에서 시간초과가 발생했을지도 모른다.

암튼 공부한 것들을 활용해 손쉽게 해결하고나니 별것 아닌데도 뿌듯하다.

<br/>

사실 에라토스테네스의 체는 개념만 생각나고 실제 구현 로직이 바로 떠오르지는 않았는데,

공부에서 끝내는 것이 아니라 실무에 적용을 해보거나 주기적으로 반복하는 것 또한 매우매우 중요한 것 같다.