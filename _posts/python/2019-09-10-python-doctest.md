---
title: "[python] doctest로 예제코드 테스트하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# doctest

doctest는 기본적으로 unittest, pytest처럼 테스를 위한 모듈이다.

다만 unittest, pytest등이 예외를 포함한 전체 기능을 세밀하게 검사하는 것이라면,

doctest는 간단하게 사용 예제를 테스트하는 정도의 목적으로 쓰인다.

무슨 말인지 예제를 보자.

```python
def doubler(num):
    return num * 2
```

`num` 이라는 정수를 받아서 2배로 돌려주는 간단한 함수이다.

doctest는 다음과 같이 작성하면 된다.

```python
def doubler(num):
    """
    This function returns the argument 'num' multipled by 2

    Example
    -------
    >>> a = 10
    >>> doubler(a)
    20
    """
    return num * 2
```

함수의 docstring을 적는 부분에 함께 작성해주면 되고,

명령형 인터페이스에서 실행하듯이 `>>>` 를 명시해 예제를 작성하면 된다.

물론 부가적인 설명 없이 이렇게 예제 코드만 작성해줘도 된다.

```python
def doubler(num):
    """
    >>> a = 10
    >>> doubler(a)
    20
    """
    return num * 2
```

작성한 doctest는 다음과 같이 doctest 모듈을 임포트해서 실행할 수 있다.

```python
import doctest


def doubler(num):
    """
    This function returns the argument 'num' multipled by 2

    Example
    -------
    >>> a = 10
    >>> doubler(a)
    20
    """
    return num * 2


doctest.testmod()
```

doctest 모듈을 임포트하고, testmod() 메소드를 호출해주면 된다.

스크립트를 실행했을때 아무런 출력이 없다면 doctest가 성공한 것이다.

만약 다음과 같이 잘못된 결과를 넣어주면 doctest에서 오류를 잡아준다.

```python
import doctest


def doubler(num):
    """
    This function returns the argument 'num' multipled by 2

    Example
    -------
    >>> a = 10
    >>> doubler(a)
    2000
    """
    return num * 2


doctest.testmod()
```

실제 실향 결과는 20이어야 하는데, 기대 결과를 2000으로 적어봤다.

실행해보자.

```shell
$ python doctest_sample.py
**********************************************************************
File "doctest_sample.py", line 11, in __main__.doubler
Failed example:
    doubler(a)
Expected:
    2000
Got:
    20
**********************************************************************
```

이처럼 입력한 기대값과 실제 출력된 값을 비교해주어 간단하게 디버깅이 가능하다.

<br/>

정리하면,

doctest는 class나 함수의 docstring을 작성할때 간단한 테스트를 추가할 수 있도록 지원한다.

주로 클래스나 함수의 간단한 사용 예제를 보여주기 위해 사용한다.

그 외 여러 케이스나 예외 상황에 대한 테스트는 따로 unittest, pytest 등의 모듈을 사용한다.
