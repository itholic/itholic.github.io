---
title: "[python] packing, unpacking 1 (*args)"
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

파이썬을 공부하다가 `*` 이나 `**` 을 사용한 특이한 코드를 본 적이 있을 것이다.

기본적으로 `2 * 5 (10)` 혹은 `2 ** 5  (32)` 처럼 곱과 제곱을 나타낼 때 쓰이지만,

가끔 함수의 매개변수 앞에 `*args`, `**kwargs`와 같이 사용될 때가 있다.

이 경우 `*`, `**` 키워드가 무엇을 의미하는지 알아보고자 한다.

우선 해당 포스팅에서는 `*` 먼저 알아보자.

<br/>

평소에 무심코 사용하던 print 함수를 생각해보자.

```python
  1 print("hello")  # hello
  2 print("hello", "world")  # hello world
  3 print("hello", "java", "and", "python")  # hello java and python
```

평소에 아무 생각 없이 사용하던 형태이다.

근데 한 번만 더 생각해보면, 이런 사실을 알 수 있다.

**"print 함수는 인자가 몇 개가 들어오든 상관 없이 동작한다"**

코드를 다시 보면 1번째 줄에서는 인자 1개를,  2번째 줄에서는 인자 2개, 3번째 줄에서는 인자 4개를 받았다.

<br/>

print 함수를 한 번 감싸서, 같은 기능을 하는 함수를 구현한다고 생각해보자.

```python
  1 def my_print(contents):
  2     print(contents)
  3    
  4 my_print("hello")  # hello
  5 my_print("hello", "world")  # TypeError: my_print() takes 1 positional argument but 2 were given
```

실제로 이런 함수를 만들 일은 없겠지만, 지극히 개념 이해를 위한 예시이다.

4번째 줄은 제대로 동작하지만 5번째 줄은 당연히 에러가 난다.

my_print는 인자를 하나만 받는데, 두 개의 인자를 넘겨주었기 때문이다.

일단 인자의 갯수를 가변적으로 받으려면 다음과 같이 변경해주면 된다.

```python
  1 def my_print(*contents):
  2     print(contents)
  3    
  4 my_print("hello")  # ('hello',)
  5 my_print("hello", "world")  # ('hello', 'world')
```

매개변수 'contents' 앞에 애스터리스크(*)를 붙여주었다.

실행된 내용을 보니 5번째 줄이 에러 없이 동작하고, 

전달 인자는 튜플의 형태로 함수에 전달된다는 것을 알 수 있다. (4번째 줄도 마찬가지로 튜플 형태로 출력되었다)

즉, "hello" 라는 전달 인자와 "world" 라는 전달 인자를 하나의 튜플에 담았다.

이렇게 여러개의 변수를 하나의 컨테이너 타입으로 묶어주는 개념을 패킹(packing) 이라고 한다.

마치 여러개의 물건을 하나의 박스에 패키징하듯이 말이다.

<br/>

근데 출력 형태가 별로 마음에 들지 않는다.

우리가 원하는 것은 `('hello',)`나 `('hello','world')`가 아니라, 

단순히 `hello`,` hello world`이다.

packing된 튜플을 그대로 print함수에 넘겨주었으니 당연한 일이다.

packing되어 넘어온 인자를 다시 unpacking해서 print함수를 실행해주면 된다.

<br/>

너무 당연한 말이지만, unpacking은 packing을 반대로 하는 것이다.

즉, 튜플에 담겨있는 값들을 다시 풀어서 개별 객체로 만드는 것이다.

함수에 값을 넘길때, 리스트나 튜플같이 컨테이너형 변수에 애스터리스크를 붙이면 unpacking되어 전달된다.

```python
  1 def my_print(*contents):
  2     print(*contents)
  3    
  4 my_print("hello")  # hello
  5 my_print("hello", "world")  # hello world
```

2번 라인을 보면 packing된 contents 인자를 다시 unpacking 해주었다.

출력된 결과를 보니 비로소 우리가 원하는 결과가 제대로 출력되었다.

정리하자면,

1. **my_print** 함수에는 "hello", "world" 두 개의 인자를 **packing**하여 `('hello', 'world')` 형태로 넘겨주었고,
2. **print** 함수에는 `('hello', 'world')` 를 다시 **unpacking**하여 "hello", "world" 형태로 넘겨준 것이다.
3. 즉, 특정 함수를 정의할때 "매개변수에 애스터리스크를 붙이게 되면 전달인자를 packing" 해준다.
4. 또한, 특정 함수에 값을 넘길때 "전달인자에 애스터리스크를 붙이면 전달 인자를 unpacking" 해준다.

<br/>

함수의 전달인자로 값을 넘길때  뿐만 아니라,

다음과 같이 컨테이너 객체를 간단히 unpacking해 변수에 할당할 수 있다.

```python
my_info = ['lee', '30', 'seoul']
name, age, address = my_info  # my_info의 요소가 순서대로 name, age, address에 할당됨

print(name)  # lee
print(age)  # 30
print(address)  # seoul
```

다만 이 경우는 unpacking할 변수(my_info)의 길이와 실제로 값을 받아주는 변수의 갯수가 일치해야한다.

다음과 같은 경우는 에러가 난다.

```python
my_info = ['lee', '30', 'seoul']
name, age = my_info  # ValueError: too many values to unpack
```

변수는 두 개 뿐인데, my_info에는 세 개의 값이 들어있기 때문에 "너무 많은 값을 unpack 하고 있다" 라는 에러가 발생한다.

<br/>

내가 원하는 인자 이외에 추가로 몇 개의 인자가 들어있는지 모르는 경우에는 다음과 같이 처리 할 수도 있다.

```python
# python2에서는 지원하지 않음
my_info = ['lee', '30', 'seoul', '010', 'xxxx', 'yyyy']
name, age, address, *unknowns = my_info

print(name)  # lee
print(age)  # 30
print(address)  # seoul
print(unknowns)  # ['010', 'xxxx', 'yyyy']
```

unknowns를 굳이 받지 않고 버리고싶다면 다음과 같이 언더바로 처리 할 수도 있겠다.

```python
# python2에서는 지원하지 않음
my_info = ['lee', '30', 'seoul']
name, age, address, *_ = my_info
```

<br/>

packing, unpacking은 두 개의 애스터리스크(`**` )를 이용하면 key값으로도 처리 가능한데,

이는 <a href="https://itholic.github.io/python-pack-unpack-2/" target="_blank">다음 포스팅</a> 에서 정리하도록 하겠다.
