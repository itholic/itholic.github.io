---
title: "[python] try문에서 else를 쓰는 이유는?"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# try문에서 else를 쓰는 이유

예전에 <a href="https://itholic.github.io/python-try-except/" target="_blank">try except 관련 포스팅</a>을 한 적이 있다.

당시 예제로 사용한 코드의 일부를 가져와보면,

```python
def div(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        print("ZeroDivisionError!!")
    else:
        return result
```

위와 같이 try문과 else문을 분리해놓은 코드가 있었고,

설명은 다음과 같았다.

```
값을 return하는 부분을 else문으로 뺐다.

try문의 내부에서 수행되는 코드는 try문 바깥(else 포함)에서 수행되는 코드에 비해 상대적으로 느리다.

에러를 잡기위해 내부적으로 조금이나마 로직이 추가될테니 당연한 일이다.

따라서 에러 발생의 위험이 있는 부분만 try문에 넣고,

나머지 부분은 else문으로 빼는것이 조금이나마 성능에 유리하다.
```

return 하는 부분을 else쪽으로 분리한 이유에 대하여, "성능" 에 초점을 맞추어 설명했다.

물론 이 말이 틀린 말은 아니지만,

문득 python이라면 else문을 따로 분리해 놓은 것에 대해서 좀 더 그럴듯한 이유가 있지 않을까하는 생각이 들었다.

<br/>

누군가 내 코드를 읽을때를 생각해보자.

try문에 있는 코드는 "에러가 발생할 가능성이 있으므로, 예의주시해야 하는 코드" 라는 암묵적 약속이 있다.

또한 except문에 있는 코드는 "try 문에서 기술한 코드에서 발생할 수 있는 에러를 처리하는 부분" 이라는 암묵적 약속이 있다.

예컨대, 

```python
try:
    result = a / b
    return result
except ZeroDivisionError:
    print("ZeroDivisionError!!")
```

위 코드는 else문을 사용하지 않고 try부분에 모든 코드를 기술했으며, 아무런 문제가 없다.

`result = a / b` 에서 에러가 발생하지 않는 경우에만 `return result`가 수행된다.

굳이 else문을 따로 분리할 필요가 없을 것 같다.

<br/>

하지만 한 번 더 생각해보면,

위 코드에서 `ZeroDivisionError` 가 발생할 수 있는 부분은 `result = a / b` 부분이다.

`return result` 부분은 except에서 처리하고있는 `ZeroDivisionError` 와 무관한 코드이다.

따라서 다음과 같이 코드를 분리해 작성자의 의도를 명확히 구분해두는게 더 합리적으로 다가온다.

```python
try:
    result = a / b
except ZeroDivisionError:
    print("ZeroDivisionError!!")
else:
    return result
```

코드가 짧아서 크게 와닿지 않을 수 있지만,

수백 ~ 수천 줄의 코드에서는 try ~ else 를 나누어 놓는 것이 코드에 대한 전체적인 의도를 파악하는데 훨씬 수월할 것이다.

<br/>

즉, try문에서 else를 사용하는 이유는 단순히 성능적인 이슈가 아닌,

"에러가 발생할 가능성이 있는 부분과 그렇지 않은 부분을 정확히 구분지어, 작성자의 의도를 보다 명확히 드러내기 위해서"

라고 보는 것이 좀 더 타당할 것 같다.
