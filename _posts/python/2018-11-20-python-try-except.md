---
title: "[python] try except else finally (파이썬 예외처리)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 예외처리

파이썬에서 예외처리는 기본적으로 try ~ except 문을 사용한다.

다음을 보자.

```python
def div(a, b):
    try:
        result = a / b
        return result
    except:
        print("error!")

div(10, 0)  # error!
```

분모(제수, 나누는 수)가 0이 될 수 없으므로 error가 발생한다.

하지만 이렇게만 하면 정확히 어떤 에러인지 디버깅하기가 어렵다.

다음과 같이 바꿔보자.

```python
def div(a, b):
    try:
        result = a / b
        return result
    except Exception as e:
        raise e

div(10, 0)  # ZeroDivisionError: integer division or modulo by zero
```

except 구문에 Exception을 설정하고, raise시켰더니 정확한 에러메시지가 출력되었다.

다음과 같이 특정 에러를 잡을 수도 있다.

```python
def div(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("ZeroDivisionError!!")

div(10, 0)  # ZeroDivisionError!!
```

정확히 어떤 에러인지 명시해서 잡았기때문에, 해당 에러에 특화된 처리가 가능하다.

위에서 이미 보여주었지만, 다음과 같이 별칭을 주어 처리할수도 있다.

```python
def div(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError as zde:
        print(zde)

div(10, 0)  # integer division or modulo by zero
```

다음과같이 여러가지 에러를 나열하는것도 가능하다.

하지만 이 경우에 별칭을 사용할 수 없다.

```python
def div(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError, TimeoutError, UnicodeError:
        print("error !!")

div(10, 0)  # error !!
```

물론 위 상황에서는 Timeout이나 Unicode관련된 에러가 발생할 일은 없지만,

어쨌든 try문에서 발생될 것으로 예상되는 에러를 모두 입력 가능하다.

에러 발생 여부에 상관없이 try문 종료 이전에 특정 구문을 수행하고싶으면 finally구문을 사용하면 된다.

```python
def div(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("ZeroDivisionError!!")
    finally:
        print("function div is end")

div(10, 0)
```

위 코드를 실행시키면 다음과 같이 출력된다.

```
ZeroDivisionError!!
function div is end
```

에러가 발생했지만, finally문을 수행하고 종료되었다.

에러가 발생하지 않았을 때에도 finally문은 수행된다.

또한 에러가 발생하지 않았을 경우, 특정 구문을 try문에 이어서 수행하고 싶으면 다음과 같이 하면 된다.

```python
def div(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        print("ZeroDivisionError!!")
    else:
        return result
    finally:
        print("function div is end")

div(10, 5)  # 2
```

값을 return하는 부분을 else문으로 뺐다.

try문의 내부에서 수행되는 코드는 try문 바깥(else 포함)에서 수행되는 코드에 비해 상대적으로 느리다.

에러를 잡기위해 내부적으로 조금이나마 로직이 추가될테니 당연한 일이다.

따라서 에러 발생의 위험이 있는 부분만 try문에 넣고, 

나머지 부분은 else문으로 빼는것이 조금이나마 성능에 유리하다.

마지막으로 try문의 흐름을 정리하자면 다음과 같다.

```
정상수행시 : try -> else -> finally
에러발생시 : try -> except -> finally
```


