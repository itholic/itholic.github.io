---
title: "[python] for ~ else"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 for ~ else 문

보통 else문은 if문과 함께 사용된다.

혹은 try ~ excpt 문과 함께 사용되어

try문에서 에러가 발생하지 않을 시, 이후 상황을 서술하는 경우에 사용되기도 한다.

(해당 내용에 대한 자세한 설명은 <a href="https://itholic.github.io/python-try-except/" target="_blank">여기</a>에 정리해놓았다)

<br/>

여끼까지는 아마 일반적으로 많이 알고있는 내용일 것이다.

하지만 else 키워드는 for문과 함께 사용할 수도 있다.

다음 예제를 보자.

```python
  1 import random
  2
  3 lucky_num = random.randint(1, 100)
  4 print(f"lucky_num is {lucky_num}")
  5
  6 for i in range(10):
  7     num = random.randint(1, 100)
  8     if num == lucky_num:
  9         print(f"Success")
 10         break
 11     if i == 9:
 12         print("Fail")
```

(3) 1부터 100사이의 숫자 중 하나를 랜덤으로 생성해 'lucky\_num' 변수로 선언한다.

(6~7) loop를 10번 돌면서 랜덤으로 1부터 100 사이의 숫자를 생성한다.

(8~10) 만약 랜덤으로 생성된 숫자가 lucky\_num과 같다면, "Success"를 출력, loop를 멈추고 빠져나온다.

(11~12) lucky\_num과 같은 숫자가 한 번도 생성되지 않았다면, "Fail" 을 출력한다.

위의 코드를 for ~ else 형식으로 바꾸면 다음과 같다.

```python
  1 import random
  2
  3 lucky_num = random.randint(1, 100)
  4 print(f"lucky_num is {lucky_num}")
  5
  6 for _ in range(10):
  7     num = random.randint(1, 100)
  8     if num == lucky_num:
  9         print(f"Success")
 10         break
 11 else:
 12     print("Fail")
```

for문 안에서 마지막 인덱스를 확인하던 절차가 사라졌다. (기존 코드의 11번째 부분)

대신 for문 바깥쪽에 else문을 추가해서, break가 발생하지 않았을때의 동작에 대해 기술했다.

즉, for ~ else문은 "for문에서 break가 발생하지 않았을 경우"의 동작을 else문에 적어주는 것이다.

for문 안에서 break가 발생한다면 11~12번째 줄의 else문은 실행되지 않는다.
