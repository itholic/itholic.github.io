---
title: "[python] Counter를 사용해 단어 갯수 세기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# collections.Counter

다음과 같이 1과 0으로 이루어진 리스트가 있다.

```python
numbers = [0, 0, 1, 1, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1 ,1]
```

0과 1이 각각 몇개인지 세려면 어떻게 해야할까?

다음과 같이 collections 모듈의 Counter라는 함수를 사용하면 된다.

```python
collections.Counter(numbers)  # Counter({1: 12, 0: 8})
```

이는 주석에 명시한 것과 같이 'Counter'라는 객체를 반환하는데,

numbers의 모든 원소에 대해 각 원소가 몇개씩 존재하는지 정보를 가지고있다.

딕셔너리와 동일하게 key를 사용해 value를 조회할 수 있다.

```python
counter_numbers = collcetions.Counter(numbers)
print(counter_numbers[1])  # 12
print(counter_numbers[0])  # 8
```

또한 딕셔너리와는 다르게 Counter간의 덧셈 뺄셈 연산도 가능하다.

Counter를 하나 더 만들어보자.

```python
numbers_2 = [1, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 1, 0]
counter_numbers_2 = collections.Counter(numbers_2)  # Counter({0: 10, 1: 9})
```

counter_numbers와 counter_numbers_2 를 더해보자.

counter_numbers에는 1이 12개, 0이 8개 있고,

counter_numbers_2에는 1이 9개, 0이 10개 있다.

```python
counter_numbers + counter_numbers_2  # Counter({1: 21, 0: 18})
```

1이 21개, 0이 18개 있는 리스트가 만들어졌다.

그럼 빼면 어떻게 될까?

1은 3개 남고, 0은 -2개 남을 것이다.


```python
counter_numbers - counter_numbers_2  # Counter({1: 3})
```

보다시피 연산 결과가 0 이하로 떨어지게 되면 해당 key는 Counter 객체에서 사라진다.

<br/>

## Counter로 단어 세기

Counter는 iterable한 객체에는 모두 적용 가능하다.

즉, 다음과 같이 String에도 적용 가능하다.

```python
sample_str = "abcbcbacabababacbabcabacabacbabacbabababaaacbab"
collections.Counter(sample_str)  # Counter({'a': 20, 'b': 18, 'c': 9})
```

그렇다면, 이를 응용해 특정 문자열에 속한 단어의 갯수를 골라내는 것도 가능하다.

```python
welcome = "hello python hello java hello world"
welcome_word_list = welcome.split()
collections.Counter(welcome_word_list)  # Counter({'hello': 3, 'python': 1, 'java': 1, 'world': 1})
```

이처럼 단어를 공백 기준으로 잘라 리스트에 넣고,

리스트를 Counter 객체로 만들어 각 단어별로 문장에서 등장한 빈도수를 간단히 알 수 있다.

이를 확장 응용하면 한 개의 문서에 들어있는 특정 단어의 갯수를 모두 뽑아내는 등의 유용한 작업이 가능하다.