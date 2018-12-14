---
title: "[python] 특정 키를 기준으로 값 정렬하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 특정 키를 기준으로 값 정렬하기

다음과 같은 리스트를 정렬하고 싶다.

```python
['c', 'kk', 'E', 'd', 'K', 'a', 'B', 'ee', 'e', 'aaa', 'g', 'z', 'cc', 'C', 'A', 'Z', 'ccc', 'i', 'bbb']
```

알파벳 순으로 정렬하고싶다면 그냥 sorted 메소드를 사용하면 된다.

```python
print(sorted(alphabets))

# result
# ['A', 'B', 'C', 'E', 'K', 'Z', 'a', 'aaa', 'bbb', 'c', 'cc', 'ccc', 'd', 'e', 'ee', 'g', 'i', 'kk', 'z']
```

길이순으로 정렬하고싶다면 어떻게 하면 될까?

key 옵션에 len 함수를 인자를 주어 정렬 기준으로 삼을 수 있다.

key 옵션에는 함수가 들어가며, 이는 리스트의 각 요소에 적용된다.

```python
print(sorted(alphabets, key=len))

# result
# ['c', 'E', 'd', 'K', 'a', 'B', 'e', 'g', 'z', 'C', 'A', 'Z', 'i', 'kk', 'ee', 'cc', 'aaa', 'ccc', 'bbb']
```

다음과 같은 튜플을 정렬하면 어떻게 될까?

```python
fruits_tuples = [
    ('Grape', 1200),
    ('Melon', 3000),
    ('Apple', 1000),
    ('Cherry', 2000),
    ('Banana', 700),
    ('Pineapple', 1500)
]

print(sorted(fruits_tuples))
# result
# [('Apple', 1000), ('Banana', 700), ('Cherry', 2000), ('Grape', 1200), ('Melon', 3000), ('Pineapple', 1500)]
```

튜플은 기본적으로 첫 번째 인자를 기준으로 정렬된다는 것을 알 수 있다.

그렇다면 가격별로 정렬할 수는 없을까?

```python
fruits_tuples = [
    ('Grape', 1200),
    ('Melon', 3000),
    ('Apple', 1000),
    ('Cherry', 2000),
    ('Banana', 700),
    ('Pineapple', 1500)
]

print(sorted(fruits_tuples, key=lambda fruits: fruits[1]))
# result
# [('Banana', 700), ('Apple', 1000), ('Grape', 1200), ('Pineapple', 1500), ('Cherry', 2000), ('Melon', 3000)]
```

각 요소에 1번 인덱스에 있는 값을 기준으로 정렬하도록 간단한 함수를 지정해주면 된다.
