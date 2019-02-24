---
title: "[python] pytest"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# pytest

pytest는 내장 단위테스트 모듈인 unittest와 같은 단위테스트 모듈이다.

내장 모듈은 아니고, pip으로 설치해주어야한다.

```shell
$ pip install pytest
```

참고로 pytest는 python3 버전에서만 동작한다.

사용법을 알아보자.

<br/>

우선 숫자를 받아서 2배로 리턴해주는 `doubler` 라는 함수를 정의해보자.

```python
# sample_test.py


def doubler(a):
    return a * 2

```

이번엔 `doubler` 함수의 테스트 함수를 만들어보자.

```python
# sample_test.py


def doubler(a):
    return a * 2


def test_doubler1():
    assert doubler(10) == 20

```

이 때, 테스트 함수의 이름은 반드시 `test` 를 접미사로 붙여야 한다.

또한 특이한 점은, `import pytest` 와 같이 따로 모듈을 import 할 필요가 없다는 점이다.

다음과 같이 `pytest` 명령을 통해 코드를 실행시키기만 하면 된다.

```shell
$ pytest sample_test.py
============================= test session starts ==============================
platform linux -- Python 3.6.5, pytest-4.3.0, py-1.8.0, pluggy-0.8.1
rootdir: /home/kdc, inifile:
collected 1 item

sample_test.py .                                                         [100%]

=========================== 1 passed in 0.04 seconds ===========================
```

1개의 item에 대한 테스트가 passed 되었다는 내용이 출력된다.

테스트 케이스를 좀 더 만들어서 실행해보자.

```python
# sample_test.py


def doubler(a):
    return a * 2


def test_doubler1():
    assert doubler(10) == 20


def test_doubler2():
    assert doubler(50) == 100


def test_doubler3():
    assert doubler(30) == 50


def doubler_test1():
    assert doubler(100) == 200


def doubler_test2():
    assert doubler(10) == 10

```

테스트 케이스 4개를 더 추가했다.

실행해보자.

```shell
$ pytest sample_test.py
============================= test session starts ==============================
platform linux -- Python 3.6.5, pytest-4.3.0, py-1.8.0, pluggy-0.8.1
rootdir: /home/kdc, inifile:
collected 3 items

sample_test.py ..F                                                       [100%]

=================================== FAILURES ===================================
________________________________ test_doubler3 _________________________________

    def test_doubler3():
>       assert doubler(30) == 50
E       assert 60 == 50
E        +  where 60 = doubler(30)

sample_test.py:13: AssertionError
====================== 1 failed, 2 passed in 0.26 seconds ======================
```

테스트 케이스를 총 5개 만들었는데, 3개의 아이템만 수집된 것을 볼 수 있다. (collected 3 items)

마지막 2개의 테스트 케이스는 함수명이 `test` 로 시작하지 않기때문에 pytest에서 인식하지 못한것이다.

그리고 `test_doubler3` 에서 에러가 발생했는데, 단순히 에러가 난 것이 아니라 상세한 결과를 출력해주고있다.

doubler(30) 의 기대값을 50으로 설정했었는데, 실제로는 60이 리턴되었다는 메시지가 출력되고있다.

`pytest` 를 쓰지 않고, 다음과 같이 코드를 추가해서 그냥 `python` 명령으로 실행해보면 차이를 알 수 있다.

```python
# sample_test.py


def doubler(a):
    return a * 2


def test_doubler1():
    assert doubler(10) == 20


def test_doubler2():
    assert doubler(50) == 100


def test_doubler3():
    assert doubler(30) == 50


def doubler_test1():
    assert doubler(100) == 200


def doubler_test2():
    assert doubler(10) == 10


if __name__ == "__main__":
    test_doubler1()
    test_doubler2()
    test_doubler3()
    doubler_test1()
    doubler_test2()
```

테스트 함수를 직접 실행하도록 코드를 추가했다.

실행해보자.

```
$ python sample_test.py
Traceback (most recent call last):
  File "sample_test.py", line 25, in <module>
    test_doubler3()
  File "sample_test.py", line 13, in test_doubler3
    assert doubler(30) == 50
AssertionError
```

실제 어떤 값이 리턴됐다거나 하는 디테일한 정보는 빠지고,

단순히 에러가 났다는 메시지를 출력하고 종료된다.

<br/>

pytest는 unittest와 달리 모듈의 특정 함수를 사용하지 않고 간단하게 테스트코드를 작성할 수 있다는 장점이 있다.

unittest였다면 다음과 같이 코드를 작성해야 했을 것이다.

```python
# sample_test.py
import unittest


def doubler(a):
    return a * 2


class DoublerTest(unittest.TestCase):
    def test_doubler1(self):
        self.assertEqual(doubler(10), 20)

    def test_doubler2(self):
        self.assertEqual(doubler(50), 100)

    def test_doubler3(self):
        self.assertEqual(doubler(30), 50)

    def doubler_test1(self):
        self.assertEqual(doubler(100), 200)

    def doubler_test2(self):
        self.assertEqual(doubler(10), 10)


if __name__ == "__main__":
    unittest.main()
```

다시 pytest를 이용한 테스트코드를 보면서 차이를 비교해보자.

```python
# sample_test.py


def doubler(a):
    return a * 2


def test_doubler1():
    assert doubler(10) == 20


def test_doubler2():
    assert doubler(50) == 100


def test_doubler3():
    assert doubler(30) == 50


def doubler_test1():
    assert doubler(100) == 200


def doubler_test2():
    assert doubler(10) == 10

```

unittest의 경우 `unittest.TestCase`, `assertEqual`, `unittest.main()` 같은 함수를 따로 알고있어야한다는 번거로움이 있다.

하지만 `assert*` 함수를 이용해 좀 더 테스트 의도를 명시적으로 드러낼 수 있다는 장점도 있다.

또한, 내장 모듈이기 때문에 따로 설치하지 않고 작성할 수 있다는 것도 장점이라면 장점이다.

참고로, unittest도 테스트 함수의 이름은 `test` 로 시작해야한다.

unittest 모듈의 보다 자세한 사용법은 <a href="https://itholic.github.io/python-unittest/" target="_blank">여기</a> 에 따로 포스팅 해두었으니, 참고하면 될 것 같다.
