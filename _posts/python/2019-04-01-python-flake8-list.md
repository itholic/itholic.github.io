---
title: "[python] flake8에서 뱉는 메시지의 의미"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 flake8에서 뱉는 메시지들의 의미

flake8은 파이썬에서 <a href="https://itholic.github.io/python-static-analysis/" target="_blank">정적분석</a>을 도와주는 모듈이다.

어떤 규칙이 지켜지지 않았을때, 해당 부분에 대한 수정 권고사항을 알려주는데,

직접 작업하면서 경험했던 몇 가지 메시지들의 의미를 정리해보았다.

<br/>

#### E502 the backslash is redundant between brackets

이는 두 괄호 사이에서 여러 줄의 문자열을 쓸때 역슬래시('\')를 쓰지 않아도 된다는 권고이다.

```python
def func(first_param, second_param, third_param, fourth_param, \
        fifth_param, sixth_param):
    pass
```

위 코드에서 첫번째 줄의 끝에 있는 역슬래시를 지워주면 된다.

<br/>

#### E128 continuation line under-indented for visual indent

여러 줄의 문자열을 사용할 경우, 시각적으로 알아보기 쉽도록 들여쓰기 수준을 맞추라는 권고이다.

```python
def func(first_param, second_param, third_param, fourth_param,
        fifth_param, sixth_param):
    pass
```

예를들면 위 코드에서 두 번째 줄의 'fifth\_param' 시작 위치를 첫 번째 줄의 'first\_param'과 같은 레벨로 맞춰주면 된다.

```python
def func(first_param, second_param, third_param, fourth_param,
         fifth_param, sixth_param):
    pass
```

미묘한 차이가 보이는가?

<br/>

#### E722 do not use bare 'except'

try ~ except 문을 사용할 때, except문을 쓰는 부분에 특정 에러를 명시하라는 권고이다.

```python
try:
    with open('test_file') as f:
        pass
except:
    print("Can not open file")
```

except문에 어떤 에러를 잡는 코드인지 명시되어있지 않으므로, 다음과 같이 고쳐주면 된다.

```python
try:
    with open('test_file') as f:
        pass
except IOError:
    print("Can not open file")
```

<br/>

#### E501 line too long (89 > 79 characters)

파이썬에서는 한 줄이 79자 이상 넘어가지 않기를 권고한다.

```python
sql = """ SELECT ID, TABLE_NAME, COLUMN_NAME FROM MY_SQLITE_TABLE WHERE ID = 123456789"""
```

위 코드는 89줄로, 79줄을 넘어간다.

다음과 같이 수정해주면 된다.

```python
sql = """ SELECT
              ID, TABLE_NAME, COLUMN_NAME
          FROM
              MY_SQLITE_TABLE
          WHERE
              ID = 123456789
"""
```

<br/>

#### E265 block comment should start with '# '

주석은 '# ' 과 같은 형태로 시작되어야 한다는 뜻이다.

```python
#Just Comment
```

이처럼 '#' 뒤에 한 칸을 띄지 않고 바로 주석을 달아서 발생하는 메시지이다.

다음과 같이 한 칸 띄어주면 된다.

```python
# Just Comment
```

<br/>


#### E266 too many leading '#' for block comment

위와 비슷한 권고사항으로, 주석은 한 개의 '#' 으로만 만들자는 권고사항이다.

```python
## Just Comment
```

위와 같은 상황에서 발생한다.

```python
# Just Comment
```

이렇게 해주면 해결된다.

<br/>

#### E101 indentation contains mixed spaces and tabs

들여쓰기에 스페이스와 탭이 섞여있다는 뜻이다.

육안으로는 확인하기 어려울 수 있는데,

해당 줄로 가서 확인해보면 실제로 섞여있다.

스페이스든, 공백이든,  한 가지로 통일시켜주면 된다.

<br/>

#### unexpected spaces around keyword / parameter equals

함수에 keyword argument를 넘겨줄때, 앞뒤로 공백을 쓰지 말라는 권고이다.

```python
  1 def func(name=''):
  2     print("my name is {}".format(name))
  3
  4
  5 func(name = 'lee')
```

5번 라인의 `name = 'lee'` 부분을 `name='lee'` 와 같이 붙여서 쓰라는 의미이다.

참고로 이는 함수 호출 뿐 아니라, 1번 라인에서 함수를 정의하는 부분에서도 똑같이 적용된다.

또한, 밑에도 정리해놓았지만,

변수 할당시에는 오히려 `s = 'Hello, World!'` 와 같이 '=' 앞뒤로 공백을 주기를 권고한다.

```python
  1 def func(name=''):
  2     print("my name is {}".format(name))
  3
  4
  5 func(name='lee')
```


<br/>

#### W291 trailing whitespace

코드의 끝에 공백이 포함되었다는 의미이다.

육안으로는 확인이 어려울지라도, 해당 줄을 확인해보면 맨 뒤쪽에 공백이 있는 것을 발견할 수 있을것이다.

<br/>

#### missing whitespace after ','

list같은 컨테이너 타입을 정의하거나 함수에 여러 개의 인자를 전달할 때,

각 요소를 구분짓는 콤마 뒤에 공백이 없다는 의미이다.

```python
l = [1,2,3,4,5]
```

다음과 같이 고쳐주면 해결된다.

```python
l = [1, 2, 3, 4, 5]
```

참고로 다음과 같이 콤마 앞쪽에 공백이 들어가도 권고사항이 발생한다.

```python
l = [1 , 2 , 3 , 4 , 5]
```

이 때 발생하는 권고사항은 `E203 whitespace before ','` 이다.

<br/>

#### E222 multiple spaces after operator

변수를 선언하거나 하는 부분에서 '=' 뒤쪽에 공백이 여러개 포함됐다는 의미이다.

```python
s =  'Hello, World!'
```

자세히 보면 '=' 뒤쪽에 공백이 두 개 포함되어있다.

파이썬에서는 '=' 연산자의 앞뒤로 공백 하나씩만을 포함하도록 권고한다.

```python
s = 'Hello, World!'
```

참고로 다음과 같이 '=' 연산자 앞뒤로 공백을 쓰지 않아도 권고사항이 발생한다.

```python
s='Hello, World!'
```

이 경우는 `E225 missing whitespace around operator` 권고사항이 발생한다.

<br/>

#### E302 expected 2 blank lines, found 1

이는 함수와 함수 사이에 두 개의 공백이 있으면 좋을 것 같은데, 한개만 있다는 권고사항이다.

```python
  1 def func1():
  2     pass
  3
  4 def func2():
  5     pass
```

다음과 같이 공백을 하나 더 넣어주면 해결된다.

```python
  1 def func1():
  2     pass
  3
  4 
  5 def func2():
  6     pass
```

<br/>


이 외에도 많은 권고사항을 교정(?)해 주는데,

새로운 내용이 추가되는대로 업데이트하도록 해야겠다.
