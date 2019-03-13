---
title: "[python] 대소관계 판정시 and 조건 생략하기 (a > b > c < d < e > f)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# and 조건 생략하기

오늘은 일하다가 우연히 발견한 아주 짧은 팁을 공유하고자 한다.

다음과 같은 코드가 있다고 하자.

```python
a = 1
b = 2
c = 3

print(a < b and b < c)  # True
```

예제라고 말하기도 민망할 정도로 너무 간단한 예제이다.

a가 b보다 작고, b는 c보다 작을 경우 True를 출력할 것이다.

그렇지 않을 경우 False를 출력할 것이다.

본 예제는 모든 조건을 만족하므로 True를 출력할 것이다.

여기서 포스팅을 끝내면 누군가의 소중한 30초를 빼앗은 죄로 고소를 당해도 할말이 없다.

<br/>

하지만 나는 이 예제의 새로운 표현 방법을 우연히 발견했다.

나만 몰랐던 사실일수도 있지만,

이 예제는 다음과 같이 한 줄로 나타낼 수도 있다.

```python
a = 1
b = 2
c = 3

print(a < b < c)  # True
```

a, b, c 세 변수의 대소관계 비교를 and 키워드 없이 한 번에 이어서 쓸 수 있는 것이다.

이는 훨씬 많은 변수를 사용하는 조건절에도 똑같이 적용 가능하다.

다음과 같은 코드가 있다고 하자.

```python
a = 1
b = 10
c = 2
d = 9
e = 3
f = 8
g = 4

print(a < b and b > c and c < d and d > e and e < f and f > g and g > a)  # True
```

총 7개의 변수가 있고, 이들간의 대소관계를 비교하기위해 총 6개의 and 키워드를 사용했다.

이는 다음과 같이 표현할 수 있다.

```python
a = 1
b = 10
c = 2
d = 9
e = 3
f = 8
g = 4

print(a < b > c < d > e < f > g > a)  # True
```

잘 보면 a가 처음과 끝에 두 번 등장했는데,

한 조건절 내에 같은 변수가 몇 번 등장해도 상관 없다.

신기하긴 한데, 어디에 써먹냐고 물어본다면, 나도 아직 써먹어본적은 없다.


<br/>

당장 생각나는 간단한 상황은,

아마 다음과 같이 어떤 좌표가 특정 프레임 내부에 있는지 체크하는 등의 로직을 짤 때 유용하게 사용할 수 있을 것 같다.

```python
  1 WIDTH = 100  # 프레임 가로 길이
  2 HEIGHT = 250  # 프레임 세로 길이
  3 x, y = input()  # x, y 좌표 입력
  4
  5 if (0 < x and x < WIDTH) and (0 < y and y < HEIGHT):
  6     print("in frame")
  7 else:
  8     print("out of frame")
```

물론 이정도 코드도 그렇게 복잡한건 아니지만,

다음과 같이 간소화 시킬 수 있다.

```python
  1 WIDTH = 100  # 프레임 가로 길이
  2 HEIGHT = 250  # 프레임 세로 길이
  3 x, y = input()  # x, y 좌표 입력
  4
  5 if (0 < x < WIDTH) and (0 < y < HEIGHT):
  6     print("in frame")
  7 else:
  8     print("out of frame")
```

5번라인의 조건식을 보면 코드가 한결 직관적으로 변한 것을 확인할 수 있다.