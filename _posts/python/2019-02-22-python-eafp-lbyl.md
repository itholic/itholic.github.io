---
title: "[python] EAFP, LBYL"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# EAFP, LBYL

파이썬을 공부하다가 생소한 용어를 접하게되어서 간단히 정리한다.

EAFP는 뭐고, LBYL은 뭘까?

<br/>

- EAFP
    - "It's Easier to Ask Forgiveness than Permission"
    - "허락을 구하는 것 보다 용서를 구하는 것이 쉽다"
    - 일단 수행 시키고(try), 에러가 발생하면 그때 처리한다(except)


- LBYL
    - "Look Before You Leap"
    - "누울 자리를 보고 다리를 뻗어라"
    - 어떤 코드를 실행하기 전에 에러가 발생할만한 부분의 조건을 미리 따져본다(if)

<br/>

쉽게 말해서 EAFP는 try ~ except 스타일이고,

LBYL은 if 문 스타일이다.

파이썬에서는 LBYL보다 EAFP를 권장한다. (<a href="https://www.python.org/dev/peps/pep-0463/" target="_blank">PEP-0463</a>)

<br/>

대체 둘의 차이가 뭐길래 if문보다 try ~ except를 권장하는 것일까?

다음과 같은 경우를 생각해보자.

```python
  1 name = 'lee'
  2
  3 grade_dict = {
  4     'lee': 'A',
  5     'park': 'A',
  6     'seo': 'C',
  7     'kim': 'B',
  8     'ahn': 'B'
  9     }
 10
 11 if name in grade_dict:
 12     print(grade_dict[name])
```

(1) 이름은 'lee' 이다

(3) 학생들의 이름과 성적을 각각 key, value로 가지는 딕셔너리이다.

(11~12) 딕셔너리에 'lee'라는 이름이 있다면, 이름에 해당하는 성적을 출력한다.

이는 LBYL 스타일의 코딩이다.

<br/>

얼핏 봤을때는 문제가 전혀 없어보이지만, 이렇게 생각해보자.

11번째 줄에서 'lee'가 grade\_dict의 key로 존재하는 것을 확인하고 12번째 줄로 넘어갔는데,

바로 그 찰나에 누군가 grade\_dict의 'lee' 항목을 삭제해버린 것이다.

물론 예시 코드가 좀 허접하긴 하지만,

if문에서 실행하는 코드가 조금 더 복잡한 코드라고 가정하면, 비동기 상황에서 충분히 벌어질 수 있는 상황이다.

이 경우 따로 예외처리를 해놓지 않았기때문에 그대로 프로그램이 뻗어버리는 불상사가 발생한다.

<br/>

하지만 다음과 같이 EAFP방식(try ~ except)으로 구현하면 어떨까?

```python
  1 name = 'lee'
  2
  3 grade_dict = {
  4     'lee': 'A',
  5     'park': 'A',
  6     'seo': 'C',
  7     'kim': 'B',
  8     'ahn': 'B'
  9     }
 10
 11 try:
 12     print(grade_dict[name])
 13 except KeyError:
 14     pass
```

따로 조건검사를 하지 않고 원하는 코드를 바로 실행시켰으며,

key가 없을 경우 그냥 넘어가도록 예외처리를 해놓았기때문에 프로그램이 죽는 일은 결코 발생하지 않는다.

<br/>

딕셔너리의 key를 가져오는 상황에서 발생하는 KeyError 뿐 아니라,

iterator의 다음 요소를 가져오는 상황에서 발생하는 StopIteration,

리스트나 튜플의 인덱스를 가져오는 상황에서 발생하는 IndexError 등,

해당 예제와 비슷한 문제가 발생할 수 있는 여러 상황들이 있다.

이러한 이유로 파이썬에서는 EAFP를 LBYL보다 권장하고있다고하니, 참고해두자.
