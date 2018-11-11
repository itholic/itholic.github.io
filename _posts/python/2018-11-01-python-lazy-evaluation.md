---
title: "[python] Lazy Evaluation"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# Lazy Evaluation 

만약 당신이 스터디룸에서 일하는 직원이다.

이 스터디룸은 스터디 공간뿐 아니라, 간단한 간식도 제공한다.

오후 7시에 10명이 스터디룸을 예약하고, 간식으로 컵라면을 주문해놓았다.

하지만 예약한 손님이 말하길,

"다들 바빠서 몇 명이 참석할지 모르겠네요, 최악의 경우 아무도 못갈수도 있어요 ㅠㅠ"

당신이 직원이라면 컵라면 10개를 미리 다 끓여 놓겠는가?

아니면 언제든 최대 10명까지 제공할 수 있는 상태로 준비만 해 두겠는가?

확실히 10명이 제시간에 온다는 보장이 있다면 전부 미리 물을 부어놓는게 효율적이겠지만,

이 상황은 당연히 후자가 효율적이다.

후자의 경우가 바로 Lazy Evaluation이다.

<br/>

Lazy Evaluation은 어떤 값이 실제로 쓰일 때 까지 그 값의 계산을 뒤로 미루는 동작 방식이다.

이는 <a href="https://itholic.github.io/python-generator/" target="_blank">Generator</a>라는 배경지식이 있어야 선행되어야 이해하기 수월하다.

<br/>

다음과 같이 숫자 1을 반환하는 단순한 함수가 있다.

반환하기 전에 "return 1" 이라는 문자열을 출력한다.

```python
def return_one():
    print("return 1")
    return 1 
```

그리고 다음과 같이 return_one을 10번 수행해서,

숫자 1을 10개 담는 리스트를 만들어보자.

```python
def return_one():
    print("return 1")
    return 1

print("[let's make one_list !]")
one_list = [return_one() for x in range(10)]
```

마지막으로, 만든 리스트(one_list)에서 값을 하나씩 꺼내 출력해보자.

```python
def return_one():
    print("return 1")
    return 1

print("[let's make one_list !]")
one_list = [return_one() for x in range(10)]

print("[let's print one_list !]")
for one in one_list:
    print(one)
```

출력 결과는 다음과 같다.

```
[let's make one_list !]
return 1
return 1
return 1
return 1
return 1
return 1
return 1
return 1
return 1
return 1

[let's print one_list !]
1
1
1
1
1
1
1
1
1
1
```

특별할거 없다.

one_list를 출력하기 전에 미리 함수 10번이 실행되어 값을 다 만들어 리스트에 저장해놓았다.

<br/>

그럼 똑같은 상황에서 one_list를 generator로 만들어보자.

list comprehension에서 대괄호만 소괄호로 바꾸어주면 generator expression이 된다.

<a href="https://itholic.github.io/python-comprehension/" target="_blank">comprehension & expression</a>은 따로 정리해놨으니 참고하면 될 것 같다.

코드를 보자.

```python
def return_one():
    print("return 1")
    return 1

print("[let's make one_list !]")
one_list = (return_one() for x in range(10))  # 대괄호[] 를 소괄호() 로 바꿈

print("[let's print one_list !]")
for one in one_list:
    print(one)
```

실행해보자.

```
[let's make one_list !]
[let's print one_list !]
return 1
1
return 1
1
return 1
1
return 1
1
return 1
1
return 1
1
return 1
1
return 1
1
return 1
1
return 1
1
```

차이가 보이는가?

[let's make one list !] 아래쪽에 아무것도 없다.

즉, 미리 리스트를 만들어놓지 않았다.

<br/>

첫 번째 예제에서 값을 출력했을 때에는,

one_list가 실제로 사용되든 말든 우선 값을 다 만들어놓았었다.

첫 번째 예제에서 [let's print one_list !] 이 수행되기 이전에 "return 1"이 미리 10번 수행된 것을 보면 알 수 있다.

<br/>

하지만 이를 generator로 만들어 값을 출력했을 때에는,

실제로 generator의 값을 출력하는 순간에 함수에서 값을 만들고있다.

즉, 값이 실제로 사용되지 않으면 연산 또한 하지 않으므로 시간과 메모리를 절약할 수 있다.

<br/>

예제를 너무 간단한 것을 들어 체감이 안될수도 있으니 한 개만 더 보자.

이번엔 5초를 대기했다가 1을 반환하는 예제이다.

그리고 전부 반환하지 않고, 1부터 10까지 랜덤의 횟수만큼만 반환한다.

```python
# -*- coding:utf-8 -*-

import time
import random

counter = random.randrange(1, 11)  # 1부터 10사이의 랜덤 값 생성
print("counter: {}".format(counter))

def return_one_after_five_sec():
    print("please wait for 5 seconds")
    time.sleep(5)
    print("return 1")
    return 1

print("[let's make one_list !]")
one_list = [return_one_after_five_sec() for x in range(10)]

# counter 숫자만큼 값 출력
print("[let's print one_list !]")
for item in one_list:
    counter -= 1
    print(item)
    if counter == 0:
        break
```


결과를 보자.

```
counter: 1

[let's make one_list !]
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1
please wait for 5 seconds
return 1

[let's print one_list !]
1

Process finished with exit code 0
```


counter가 1부터 10 사이의 값중 하필 1이 생성되었고,

덕분 50초에 걸쳐 리스트를 미리 만들어 놨는데 단 한개의 값만 사용했다.

라면을 10개 다끓여놨는데 스터디룸에 한 명 밖에 안와서 나머지 9개는 버렸다 ㅜㅜ

<br/>

이런 상황에서는 연산 결과의 목록을 list보다는 generator로 만들어놓는게 효율적이다.

완전히 같은 상황을 generator로 바꿔보자.

대괄호만 소괄호로 바꾸면 된다.

```python
# -*- coding:utf-8 -*-

import time
import random

counter = random.randrange(1, 11)  # 1부터 10사이의 랜덤 값 생성
print("counter: {}".format(counter))

def return_one_after_five_sec():
    print("please wait for 5 seconds")
    time.sleep(5)
    print("return 1")
    return 1

print("[let's make one_list !]")
one_list = (return_one_after_five_sec() for x in range(10))  # generator 생성

# counter 숫자만큼 값 출력
print("[let's print one_list !]")
for item in one_list:
    counter -= 1
    print(item)
    if counter == 0:
        break
```

결과는 어떨까?

```
counter: 1
[let's make one_list !]
[let's print one_list !]
please wait for 5 seconds
return 1
1
```

마찬가지로 counter 값은 1이 생성되었다.

하지만 미리 리스트를 만들어놓지 않은 덕분에 5초만에 작업을 끝내고 프로그램이 종료되었다.

미리 라면을 끓여놓지 않길 잘한것이다.

<br/>

이처럼 Lazy Evaluation을 적절히 활용하면,

라면을 미리 다 끓여놓았다가 아무도 오지 않아서 다 버려야하는 상황을 방지할 수 있다.

시간을 들여 연산하고 메모리까지 할당해 놓았는데,

프로그램이 종료될때까지 사용되지 않으면 억울하니까 Lazy Evaluation을 적절히 활용하자.

<br/>

하지만 모든 요소, 혹은 대부분의 요소가 사용될 것이 확실한 상황이라면,

list를 통해 미리 연산을 해 두는 것이 더 효율적이므로 아무 상황에서나 남발하지는 말자.
