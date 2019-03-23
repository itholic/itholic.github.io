---
title: "[python] 문자열 거꾸로 출력하기 [::-1]"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 문자열 거꾸로 출력하기

'abcde' 라는 문자열을 거꾸로 출력해보자.

즉, 'edcba' 라는 출력을 원한다.

무수히 많은 방법이 있겠지만, 몇 가지만 살펴보자.

일단 단순히 for문을 통해 해결하는 방법이 있을것이다.

```python
s = 'abcde'
s_reverse = ''  # 기존 문자열을 역순으로 담아줄 빈 문자열 선언
for char in s:
    s_reverse = char + s_reverse

print(s_reverse)  # edcba
```

s\_reverse라는 빈 문자열을 선언하고,

기존 문자열에서 문자를 차례대로 가져와 앞뒤 순서를 바꾸어주었다.

<br/>

이번엔 파이썬에서 제공하는 함수를 사용해보자.

우선 다음과 같이 reverse를 활용하는 방법이 있을것이다.

```python
s = 'abcde'
s_list = list(s)  # reverse 함수를 사용하기 위해 문자열을 list로 치환
s_list.reverse()  # reverse 함수를 사용해 문자열 리스트를 거꾸로 뒤집음

print(''.join(s_list))  # 거꾸로 뒤집어진 리스트를 연결해서 출력
```

정상적으로 동작하지만 개인적으로 뭔가 깔끔하지 못한 느낌이 든다.

이번엔 reversed를 활용해보자.

```python
s = 'abcde'
print(''.join(reversed(s)))  # 'edcba'
```

reversed는 reverse와는 달리 문자열에도 바로 적용이 가능하므로, (reverse는 list에만 사용 가능)

reversed(s)를 통해 문자열을 거꾸로 뒤집은 후 join으로 연결해 바로 출력해주었다.

<br/>

한 줄로 끝나버렸으니 여기서 더 단순화할 수 없을 것처럼 보인다.

하지만 파이썬에선 이런것도 가능하다.

```python
s = 'abcde'
print(s[::-1])  # 'edcba'
```

문자열을 [::-1] 이라는 인덱스로 호출하면,

아주 단순하게 해당 문자열을 뒤집은 결과를 반환한다.

만약 [3:0:-1] 이라는 인덱스로 호출하면,

3번 인덱스부터 1번 인덱스까지(0번 까지가 아님) 역순으로 출력해준다.

```python
s = 'abcde'
print(s[3:0:-1])  # dcb
```

[3::-1] 과 같이 출력하면 3번 인덱스부터 0번 인덱스까지 역순으로 출력해준다.

```python
s = 'abcde'
print(s[3::-1])  # dcba
```

[4::-1] 은 4번 인덱스부터 0번 인덱스까지 역순으로 출력해주는데,

이 때 4번 인덱스가 마지막 인덱스라면 생략할 수 있다.

```python
s = 'abcde'
print(s[4::-1])  # edcba
print(s[::-1])  # edcba
```

그래서 결과적으로 [::-1] 인덱스를 주면 전체 문자열을 역순으로 출력해주는 것이다.

문자열 뿐 아니라 리스트나 튜플에도 적용 가능하다.

```python
l = ['a', 'b', 'c', 'd', 'e']
print(l[::-1])  # ['e', 'd', 'c', 'b', 'a']

t = ('a', 'b', 'c', 'd', 'e')
print(t[::-1])  # ('e', 'd', 'c', 'b', 'a')
```

