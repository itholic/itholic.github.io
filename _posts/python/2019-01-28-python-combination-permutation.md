---
title: "[python] itertools를 이용해 순열과 조합 구하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# itertools를 이용해 순열과 조합 구하기

A, B, C 라는 세 개의 문자가 있다. 

이 문자들중 두 개를 무작위로 뽑았을때의 순열과 조합은 어떻게 구하면 될까?

<br/>

순열은 AB, AC, BA, BC, CA, CB 가 될 것이고,

조합은 AB, AC, BC 가 될 것이다.

<br/>

프로그래밍을 통해 구하려면 이러한 조합들을 찾아내는 함수를 작성해서 구해야 할 것이다.

하지만 파이썬에서는 이를 간단하게 계산해주는 모듈을 제공한다.

바로 itertools의 permutations 과 combinations이다.

```
import itertools

chars = ['A', 'B', 'C']

p = itertools.permutations(chars, 2)  # 순열
c = itertools.combinations(chars, 2)  # 조합
```

위와 같은 코드를 실행하게 되면,

p에는 `itertools.permutations` 객체가,

c에는 `itertools.combinations` 객체가 반환된다.

두 번째 인자로 받는 숫자(2)는 주어진 컨테이너 타입 변수에서 몇 개의 아이템을 조합할지 결정하는 인자이다.

참고로 permutations는 두 번째 인자를 받지 않으면 컨테이너의 전체 길이(위 예제에서는 3)가 default로 들어가고,

combinations는 두 번째 인자를 받지 않으면 동작하지 않는다(에러)

이를 list로 만들어서 출력해보자.


```
import itertools

chars = ['A', 'B', 'C']

p = itertools.permutations(chars, 2)  # 순열
c = itertools.combinations(chars, 2)  # 조합

print(list(p))
print(list(c))
```

실행 결과는 다음과 같다

```
[('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
[('A', 'B'), ('A', 'C'), ('B', 'C')]
```

순열과 조합이 정상적으로 출력된 것을 확인할 수 있다.
