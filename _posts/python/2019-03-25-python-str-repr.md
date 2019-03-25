---
title: "[python] str, repr 차이"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 str, repr 차이

파이썬에서 str과 repr의 차이는 무엇일까?

간단한 예제를보자.

```python
s = "Hello, World!"

print(str(s))  # Hello, World!
print(repr(s))  # 'Hello, World!'
```

s라는 변수에 "Hello, World" 라는 문자열을 할당했다.

s를 str로 출력하니 `Hello, World!` 가 출력되었고,

s를 repr로 출력하니 `'Hello, World!'` 와 같이 따옴표로 감싸져서 출력이되었다.

<br/>

이게 무슨 차이일까?

repr로 출력하면, '파이썬에서 해당 객체를 만들 수 있는 문자열'로 출력된다. (이를 '공식적인' 문자열이라 한다)

<br/>

그럼 이게 또 무슨말일까?

간단한 실험을 해보자.

str로 출력된 `Hello, World!` 를 그대로 복사해서 s와 같은 객체를 만들 수 있는가?

```python
s = Hello, World!

print(s)
```

위 코드를 실행하면 당연히 다음과 같은 에러가난다.

```
  File "<stdin>", line 1
    s = Hello, World!
                    ^
SyntaxError: invalid syntax
```

즉, s라는 변수를 str로 출력한 문자열로는 다시 s와 같은 객체를 만들 수 없다.

<br/>

그렇다면, s를 repr로 출력한 `'Hello, World!'` 를 그대로 복사해서 s와 같은 객체를 만들 수 있는가?

```python
s = 'Hello, World!'

print(s)  # Hello, World!
```

보다시피 만들 수 있다.

즉, 특정 객체에 대하여 repr이 리턴한 문자열은 '파이썬으로 해당 객체를 만들 수 있게 해주는 공식적인 문자열'이다.

<br/>

한 가지 예제를 더 보자.

```python
a = 0.12345678987654321

print(str(a))  # 0.123456789877
print(repr(a))  # 0.12345678987654321
```

str을 통해 a를 출력하면 소숫점 13번쨰 자리에서 반올림하여 12번쨰 자리까지만 출력된다.

당연히 뒤쪽이 짤려있으므로, 이 문자열로는 a와 같은 객체를 다시 만들 수 없다.

하지만 repr을 통해 a를 출력하면 처음 a를 만들었을때 할당한 모든 값이 전부 그대로 출력된다.

즉, repr을 통해 출력한 문자열로는 다시 기존 객체와 같은 값을 가지는 객체를 생성할 수 있다.
