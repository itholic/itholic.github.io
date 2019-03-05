---
title: "[python] packing, unpacking 2 (**kwargs)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# packing, unpacking

<a href="https://itholic.github.io/python-pack-unpack-1/" target="_blank">지난 포스팅</a>에서 `*`을 활용한 패킹/언패킹을 정리했었다.

이번에는 key를 활용해 패킹/언패킹을 할 수 있게 해주는 키워드인 `**`를 알아보자.

<br/>

다음과 같이 회원의 이름과 나이를 키워드 인자로 받아서 출력해주는 함수가 있다고 하자.

```python
  1 def print_customer_info(name, age):
  2     print(f"name: {name}")
  3     print(f"age: {age}")
  4
  5
  6 print_customer_info(name='lee', age='30')
```

실행해보자.

```
name: lee
age: 30
```

잘 동작한다.

근데, 회원 정보에 '주소' 라는 항목이 추가되면 어떻게 될까?

```python
  1 def print_customer_info(name, age, address):
  2     print(f"name: {name}")
  3     print(f"age: {age}")
  4     print(f"address: {address}")
  5
  6
  7 print_customer_info(name='lee', age='30', address='seoul')
```

매개변수에 주소를 받을 변수 address를 추가하고, 구현부에서도 이를 출력하는 부분을 추가해야한다. (1, 4 번 라인)

이런식으로 정보가 하나 추가 될 때마다 귀찮은 작업이 반복될 것이다.

그렇다면, 함수의 변경 없이, 전달받는 키워드 인자의 갯수에 상관 없이 처리 할 수는 없을까?

다행히도 방법이 있다.

`**`를 활용해 함수에 전달해주는 키워드 인자를 packing 해서 넘겨주면 된다.

말이 어려우니 예제를 보자.

```python
  1 def print_customer_info(**kwargs):
  2     print(kwargs)
  3
  4
  5 print_customer_info(name='lee', age='30')  # {'name': 'lee', 'age': '30'}
  6 print_customer_info(name='lee', age='30', address='seoul')  # {'name': 'lee', 'age': '30', 'address': 'seoul'}
```

name, age, address와 같은 매개변수들 대신 `**kwargs` 로 바꿔주었다.

그리고 어떤 값이 전달되는지 출력해보았다.

결과는, 넘겨준 키워드 인자가 딕셔너리 형태로 변경되어 함수에 전달되는 것을 확인할 수 있다. (5,6번 라인 주석 확인)

그렇다면 기존의 함수는 최종적으로 다음과 같은 형태로 개선될 수 있다.

```python
  1 def print_customer_info(**kwargs):
  2     for key in kwargs:
  3         print(f"{key}: {kwargs[key]}")
  4
  5
  6 print_customer_info(name='lee', age='30')
  7 print_customer_info(name='lee', age='30', address='seoul')
```

kwargs가 딕셔너리 형태로 넘어오므로,

딕셔너리를 iteration돌면서 key, value를 뽑아 출력해주면 기존과 똑같은 기능을 확장성있게 구현할 수 있다.

unpacking을 할 때에는 <a href="https://itholic.github.io/python-pack-unpack-1/" target="_blank">이전 포스팅</a>에서 `*`를 사용했을때와 마찬가지로,

함수에 값을 넘길때 딕셔너리에 `**`를 붙여주면 된다.

```python
  1 def print_name_age_addr(name, age, addr):
  2     print(f"name: {name}")
  3     print(f"age: {age}")
  4     print(f"addr: {addr}")
  5
  6
  7 my_dict = {
  8         'name': 'lee',
  9         'age': '30',
 10         'addr': 'seoul'
 11     }
 12
 13 print_name_age_addr(**my_dict)
```

name, age, addr를 받는 `print_name_age_addr` 함수가 있다.

이 세개의 변수를 키워드로 가지는 딕셔너리를 한 번에 넘겨줄때 `**`을 활용해 딕셔너리를 unpacking해주면 된다.

만약 unpacking을 사용하지 않으면, 다음과 같이 넘겨줘야한다.

```python
  1 def print_name_age_addr(name, age, addr):
  2     print(f"name: {name}")
  3     print(f"age: {age}")
  4     print(f"addr: {addr}")
  5
  6
  7 my_dict = {
  8         'name': 'lee',
  9         'age': '30',
 10         'addr': 'seoul'
 11     }
 12
 13 print_name_age_addr(my_dict['name'], my_dict['age'], my_dict['addr'])
```

13번 라인을 비교해보면 딕셔너리 unpacking을 사용하는게 왜 편리한지 알 수 있다.
