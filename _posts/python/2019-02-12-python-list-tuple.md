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

그래서 딱히 list와 tuple의 차이점을 고려하지 않고 그냥 자주 쓰던것을 종종 사용하곤 했다.

하지만 몇몇 상황에서 list를 선택하는지 tuple을 선택하는지에 따라 다른 결과를 볼 수도 있다.

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
various_tuple = ("GoodBye", [2016, 2017, 2018])
my_dict = {various_tuple: "My tuple!"}  # TypeError: unhashable type: 'list'
```

참고로,

다음과 같이 문자열 또한 불변한 객체이기 때문에 딕셔너리의 키 값으로 사용할 수 있는 것이다.

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

데이터가 정렬되어있지 않고, 데이터의 복잡도가 높을수록 차이가 더 많이 나는 것 같다

(몇 번의 테스트 결과 그렇게 확인 되었는데, 혹시 아니라면 댓글 달아주시면 감사하겠습니다)


#### 4. 객체를 복사하는 방식의 차이 (190219 추가)

list의 경우, 다음과 같은 방식들로 객체를 복사할 경우 서로 Identity가 다른 객체로 복사된다.

즉, is 로 비교를 했을때 같은 객체가 아닌 새로운 객체가 생긴다는 뜻이다.

1. 슬라이싱(`[:]`) 을 이용한 복사

```python
>>> l1 = [1, 2, 3]
>>> l2 = l1[:]
>>> l1 is l2
False
```

2. `list()` 메소드를 이용한 복사

```python
>>> l1 = [1, 2, 3]
>>> l2 = list(l1)
>>> l1 is l2
False
```

하지만 tuple의 경우, 동일한 방식으로 복사할 경우 서로 Identity가 같은 객체로 복사된다.

즉, list처럼 새로운 메모리에 값을 할당하는 것이 아니라,

복사된 변수가 원본과 같은 객체를 가리키고있다는 뜻이다.

1. 슬라이싱(`[:]`) 을 이용한 복사

```python
>>> t1 = (1, 2, 3)
>>> t2 = t1[:]
>>> t1 is t2
True
```

2. `tuple()` 메소드를 이용한 복사

```python
>>> t1 = (1, 2, 3)
>>> t2 = tuple(t1)
>>> t1 is t2
True
```

이는 파이썬에서 메모리를 절약하고 성능을 높이기 위한 일종의 전략이다.

어차피 tuple은 불변객체이므로 값을 바꿀 수 없다.

따라서 원본이나 사본의 값을 바꾸었을때, 반대편의 값도 함께 바뀌는 것에 대한 걱정을 할 필요가 없다.

그래서 객체를 굳이 복사하지 않고 기존의 객체에 변수만 할당하는 식으로 효율을 높이는 것이다.

<br/>

참고로 `is` 비교와 `==` 비교의 차이는 따로 정리해두었으니,

혹시 Equality 와 Identity의 개념이 생소한 사람은 <a href="https://itholic.github.io/python-identity-equality/" target="_blank">여기</a>를 클릭해서 참고해도 좋을 것 같다.
