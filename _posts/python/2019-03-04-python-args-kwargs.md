---
title: "[python] \*args, \*\*kwargs"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# \*args, \*\*kwargs

- 관련 포스팅
-- \* 사용법: <a href="https://itholic.github.io/python-pack-unpack-1/" target="_blank">packing, unpacking 1</a>
-- \*\* 사용법: <a href="https://itholic.github.io/python-pack-unpack-1/" target="_blank">packing, unpacking 2</a>

positional arguments(args)와 keyword arguments(kwargs)의 개념과 사용 방법은 위에 링크를 걸어놓은 두 개 포스팅을 통해 간단히 정리해보았다.

그럼, 이 두개를 같이 사용하면서 packing, unpacking의 개념을 마지막으로 정리해보고, 주의할 점에 대해서도 알아보자.

### 사용법

```python
  1 def args_kwargs(*args, **kwargs):
  2     print(f"args: {args}")
  3     print(f"kwargs: {kwargs}")
  4
  5
  6 args_kwargs(1, 2, 3, 4, 5, {"name": "lee", "age": "30", "addr": "seoul"})
```

args와 kwargs를 받는 함수 args\_kwargs를 정의했다.

그리고 숫자 1, 2, 3, 4, 5와 키워드 인자로 사용할 딕셔너리를 넘겨주었다.

실행시켜보자.

```
args: (1, 2, 3, 4, 5, {'name': 'lee', 'age': '30', 'addr': 'seoul'})
kwargs: {}
```

뭔가 이상하다.

kwargs에는 아무것도 들어가지 않고,

args에 모든 값이 다 들어가버렸다.

keyword arguments를 positional arguments와 함께 사용하려면 다음과 키워드를 명시해서 호출해야한다.

```python
  1 def args_kwargs(*args, **kwargs):
  2     print(f"args: {args}")
  3     print(f"kwargs: {kwargs}")
  4
  5
  6 args_kwargs(1, 2, 3, 4, 5, kwargs={"name": "lee", "age": "30", "addr": "seoul"})
```

6번 라인을 보면, kwargs에 넘길 값을 정확히 명시하고있다.

이렇게 하지 않으면 모두 args로 인식되어버린다.

실행해보자.

```
args: (1, 2, 3, 4, 5)
kwargs: {'kwargs': {'name': 'lee', 'age': '30', 'addr': 'seoul'}}
```

args와 kwargs에 의도한대로 잘 들어갔다.

<br/>

### 주의사항

1. keyword arguments는 positional arguments보다 앞에 올 수 없다.


```python
  1 def args_kwargs(**kwargs, *args):
  2     pass
```

kwargs를 args보다 앞쪽에 배치했다.

이 코드를 실행하면 다음과 같은 에러가 난다.

```
    def args_kwargs(**kwargs, *args):
                              ^
SyntaxError: invalid syntax
```

**positional arguments와 keyword arguments를 함께 사용할 때에는 반드시 positional arguments가 먼저 와야한다.**


<br/>

2. positional argument(일반 변수), positional arguments, keyword arguments를 같이 사용하는 경우.

```python
  1 def args_kwargs(arg1, arg2, *args, **kwargs):
  2     print(f"arg1: {arg1}")
  3     print(f"arg2: {arg2}")
  4     print(f"args: {args}")
  5     print(f"kwargs: {kwargs}")
  6
  7
  8 args_kwargs(1, 2, 3, 4, 5, kwargs={"name": "lee", "age": "30", "addr": "seoul"})
```

args, kwargs 앞에 일반 변수 arg1, arg2를 추가했다.

실행해보자.

```
arg1: 1
arg2: 2
args: (3, 4, 5)
kwargs: {'kwargs': {'name': 'lee', 'age': '30', 'addr': 'seoul'}}
```

우선 일반 변수의 갯수만큼 순서대로 전달 인자를 할당하고,

남는 인자들은 args에 packing해서 전달했다.

이 경우도 반드시 positional argument(일반 변수), positional arguments, keyword arguments의 순서대로 선언해야한다.

<br/>

3. 한 개의 함수에서 두 개 이상의 arguments 혹은 keyword arguments를 사용할 수 없다.


```python
  1 def args_kwargs(*args1, *args2):
  2     pass
```

```python
  1 def args_kwargs(**kwargs1, **kwargs2):
  2     pass
```

위 두 개 코드는 모두 에러가 난다.

**positional arguments와 keyword arguments는 한 개의 함수에서 두 개 이상 선언할 수 없다.**
