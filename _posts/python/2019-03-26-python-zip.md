---
title: "[python] zip"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 zip

파이썬에는 zip이라는 내장함수가 있다.

for loop에서 iteration을 돌릴때 종종 등장하는데, 어떤 용도인지 알아보자.

```python
name_tuple = ('lee', 'park', 'kim')
score_tuple = ('100', '80', '90')
```

위와 같은 두 개의 튜플이 있을때,

이 튜플들을 가지고 딕셔너리를 만들어보자.

name을 key로 가지고, score를 value로 가지는 딕셔너리이다.

key - value는 각각 동일한 인덱스에 매칭된다고 가정하자.

즉, lee는 100점, park은 80점, kim은 90점이다.

<br/>

우선 zip을 쓰지 않고 그냥 만들어보자.

```python
name_tuple = ('lee', 'park', 'kim')
score_tuple = ('100', '80', '90')

score_dict = {}
for i in range(len(name_tuple)):
    score_dict[name_tuple[i]] = score_tuple[i]

print(score_dict)  # {'park': '80', 'lee': '100', 'kim': '90'}
```

score\_dict라는 빈 딕셔너리를 선언하고,

name\_tuple의 길이만큼 for loop을 돌며,

name\_tuple의 요소는 key로, score\_tuple의 요소는 value로 할당해주었다.

이 방법도 나쁘지는 않지만, zip을 쓰면 훨씬 깔끔하고 직관적인 코드를 작성할 수 있다.

```python
name_tuple = ('lee', 'park', 'kim')
score_tuple = ('100', '80', '90')

score_dict = {}
for name, score in zip(name_tuple, score_tuple):
    score_dict[name] = score

print(score_dict)  # {'park': '80', 'lee': '100', 'kim': '90'}
```

for loop 부분을 보면, name\_tuple과 score\_tuple을 zip으로 묶어주었다.

그리고 for loop 내부에서는 name, score라는 이름으로 각 요소를 가져다가 사용하고있다.

zip은 인자로 받은 iterable한 객체들의 각요소를 튜플로 묶어서 반환해준다.

다음 예제를 보면 이해가 쉽게 될 것이다.

```python
name_tuple = ('lee', 'park', 'kim')
score_tuple = ('100', '80', '90')

for name, score in zip(name_tuple, score_tuple):
    print(name, score)
```

위 코드를 실행한 결과는 다음과 같다.

```
('lee', '100')
('park', '80')
('kim', '90')
```

참고로 zip 함수는 2개뿐만 아니라 3개 이상의 값을 넣어 사용하는 것도 가능하다.

```python
name_tuple = ('lee', 'park', 'kim')
score_tuple = ('100', '80', '90')
gender_tuple = ('male', 'female', 'male')
addr_tuple = ('seoul', 'busan', 'daejeon')

for name, score, gender, addr in zip(name_tuple, score_tuple, gender_tuple, addr_tuple):
    print(name, score, gender, addr)
```

위 코드의 결과는 다음과 같다.

```
('lee', '100', 'male', 'seoul')
('park', '80', 'female', 'busan')
('kim', '90', 'male', 'daejeon')
```
