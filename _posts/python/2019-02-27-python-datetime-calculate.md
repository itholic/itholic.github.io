---
title: "[python] datetime을 이용해 시간, 날짜 더하고 빼기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# datetime을 이용해 시간, 날짜 더하고 빼기

날짜를 다루다보면,

특정 시간을 기준으로 '몇시간 후', '혹은 며칠 전'과 같은 데이터를 얻고싶을 때가 있다.

예를들어 지금 이순간부터 777일 후는 몇월 며칠일까?

매 월마다 날짜수가 다르고, 또 2월은 해마다 날짜수가 다르기때문에 계산을 하려면 골치아프다.

하지만 datetime 모듈을 쓰면 다음과 같이 아주 간단하게 해결 가능하다.

```python
  1 import datetime
  2 
  3 now = datetime.datetime.now()
  4 now_after_777 = now + datetime.timedelta(days=777)
  5 
  6 print(now_after_777)  # 2021-04-14 21:15:54.891525
```

(3) `datetime.datetime.now()` 는 현재 시간을 가져온다.

(4) `datetime.timedelta(days=777)` 은 777일을 의미한다.

이를 단순히 앞서 구한 현재 시간에 더해주면, 777일 후가 언제인지 알아서 정확하게 계산해준다.

`days` 외에 `seconds, microseconds, milliseconds, minutes, hours, weeks` 도 가능하니 입맛에 맞게 고르면된다.

<br/>

만약 현재시간이 아닌 특정 날짜를 기준으로 계산하고 싶다면?

datetime의 도움을 받아 아주 간단히 특정 날짜의 데이터를 만들어 계산해주면 된다.

이번에는 미래가 아닌 과거의 시간을 찾아보자.

"2002년 2월 2일의 7777일 전"이 언제였는지 계산해볼까?

```python
  1 import datetime
  2
  3 day = datetime.datetime(2002,2,2)
  4 day_before_7777 = day - datetime.timedelta(days=7777)
  5
  6 print(day_before_7777)  # 1980-10-18 00:00:00
```

무려 1980년 10월 18일이다.

나같은 경우 실무에서 생각보다 자주 사용하게되는 기능이라서,

오늘도 쓰게된 김에 정리를 해보았다.
