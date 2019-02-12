---
title: "[python] 파이썬 list와 tuple의 차이"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 list, tuple 차이

list와 tuple은 얼핏보면 상당히 비슷하다.

그래서 딱히 list와 tuple의 차이점을 고려하지 않고 그냥 자주 쓰던것을 종종 사용하곤 한다.

하지만 몇몇 상황에서 list를 선택하는지 tuple을 선택하는지에따라 다른 결과를 볼 수도 있다.

list와 tuple의 공통점과 차이점을 간단히 알아보자.

## 공통점

#### 1. list와 tuple모두 여러 데이터를 담을 수 있는 컨테이너형 변수이다.

```python
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
my_tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```

#### 2. list와 tuple 모두 인덱스를 통해 특정 요소에 접근할 수 있다.

```python
my_list[0]  # 1
my_tuple[0]  # 1
```

#### 3. list와 tuple 모두 iterable하다. 즉, for문에 넣고 돌릴 수 있다.

```python
for item in my_list:
    pass

for item in my_tuple:
    pass
```


## 차이점

#### 1. list는 mutable(가변)하지만 tuple은 immutable(불변)하다.

```python
my_list[0] = "Hello"  # various_list = ["Hello", 2, 3, 4, 5, 6, 7, 8, 9, 10]
my_tuple[0] = "Hello"  # TypeError: 'tuple' object does not support item assignment
```

#### 2. 따라서, list는 딕셔너리의 key값(해쉬값)으로 쓸 수 없지만, tuple은 가능하다.

```python
my_dict = {my_list: "My List!"}  # TypeError: unhashable type: 'list'
my_dict = {my_tuple: "My tuple!"}  # 정상 작동
```

딕셔너리의 키값은 불변한(immutable) 값만 올 수 있기 때문이다.

하지만, 만약 다음과 같이 튜플에 리스트가 들어있는 경우라면 이 경우는 키 값으로 사용할 수 없다.

```python
various_tuple = ["GoodBye", [2016, 2017, 2018]]
my_dict = {various_tuple: "My tuple!"}  # TypeError: unhashable type: 'list'
```


참고로 문자열 또한 불변한 값이기 때문에 키값으로 사용할 수 있는 것이다.

```python
my_string = "Hello"
my_string[0] = "B"  # TypeError: 'str' object does not support item assignment
```


#### 3. iteration을 도는 속도가 튜플이 더 빠르다.

```python
  1 import time
  2
  3 big_list = [num for num in range(10000000)]
  4 big_tuple = tuple([num for num in range(10000000)])
  5
  6 start = time.time()
  7
  8 for num in big_list:
  9     pass
 10
 11 print("list iteration: {}".format(time.time() - start))
 12
 13 start = time.time()
 14
 15 for num in big_tuple:
 16     pass
 17
 18 print("tuple iteration: {}".format(time.time() - start))
```

1000만건의 숫자를 각각 list와 tuple에 넣고 for문을 돌려 수행시간을 측정했다.

결과는 다음과 같다.

```
list iteration: 1.21506929397583
tuple iteration: 1.0440597534179688
```

만약 데이터가 정렬되어있지 않고, 데이터의 복잡도가 높을수록 차이가 더 많이 나는 것 같다

(몇 번의 테스트 결과 그렇게 확인 되었는데, 혹시 아니라면 댓글 달아주시면 감사하겠습니다)

