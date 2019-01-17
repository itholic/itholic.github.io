---
title: "[python] re - 정규표현식 대소문자 구분없이 매칭하기(컴파일 옵션)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# re 모듈로 대소문자 구분없이 찾아내기

파이썬에서 정규표현식을 활용할때 re모듈을 주로 사용한다.

다음과 같은 SQL 에서 CONTAINS함수의 인자로 받는 `GEOMFROMTEXT('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))')` 부분만 뽑으려면 어떻게 해야할까?

```sql
SELECT
    * 
FROM
    TEST_TABLE
WHERE
    CONTAINS(GEOMFROMTEXT('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))'), a);
```

함수의 인자 부분에는 `POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))` 이외의 여러 문자열이 올 수 있음을 감안하자.

다음과 같이 re모듈을 사용해 규칙을 만들어주면 된다.

```python
import re

query = "SELECT * FROM LOCAL_TEST_TABLE WHERE CONTAINS(GEOMFROMTEXT('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))'), a);"

p = re.compile("(\s*GEOMFROMTEXT.+'\s*\)\s*),")

feature = p.findall(query)

print(feature)
```

실행하면 다음과 같이 해당 부분 문자열을 출력하는 것을 확인할 수 있다.

```
["GEOMFROMTEXT('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))')"]
```

근데 이때, 만약 GEOMFROMTEXT 라는 부분이 'geomfromtext'와 같이 소문자로 들어온다면?

혹은 대소문자가 섞인 'GeomFromText' 형태로 들어온다면?

확인해보자.

```python
import re

query = "SELECT * FROM LOCAL_TEST_TABLE WHERE CONTAINS(GeomFromText('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))'), a);"

p = re.compile("(\s*GEOMFROMTEXT.+'\s*\)\s*),")

feature = p.findall(query)

print(feature)
```
```
[]
```

문자열을 찾지 못했다.

이는 compile쪽에서 규칙을 만들때 대문자 스트링을 그대로 박아놨기 때문이다.

그렇다면 모든 상황을 고려해서 `GEOMFROMTEXT|geomfromtext|GeomFromText` 와 같이 처리해야할까?

만약 어떤 변태같은 사람이 `GeOmFrOmTeXt` 와 같이 쿼리한다면? (만약 실제로 있다면 가까이 지내지 말자)

대소문자 구분없이 문자열을 찾아내려면 단순히 다음과 같이 처리 주면 된다.

```python
0  import re
1  
2  query = "SELECT * FROM LOCAL_TEST_TABLE WHERE CONTAINS(GeomFromText('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))'), a);"
3  
4  p = re.compile("(\s*GEOMFROMTEXT.+'\s*\)\s*),", re.I)
5  
6  feature = p.findall(query)
7
8. print(feature)
```

4번라인을 잘 보면 compile함수로 규칙을 만드는 부분에서 `re.I`옵션을 준것을 확인할 수 있다.

실행하면 다음과 같이 대소문자 가리지 않고 찾아낸다.

```
["GeomFromText('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0))')"]
```

이 때, `re.I`와 같이 컴파일시 옵션으로 주는 인자들을 '컴파일 옵션' 이라한다.

<br/>

참고로 re모듈에서는 `re.I` 이외에도 다음과 같은 컴파일 옵션들을 제공한다.

1. `re.I` 혹은 `re.IGNORECASE`
    - 대소문자 구분없이 매칭한다
2. `re.S` 혹은 `re.DOTALL`
    - 정규식의 . 메타문자가 개행문자(\n)도 함께 매칭한다.
    - 해당 옵션이 없다면, . 메타문자는 개행문자를 제외한 모든 문자와 매칭된다.
3. `re.M` 혹은 `re.MULTILINE`
    - ^ 혹은 $ 메타문자를 모든 라인마다 적용한다.
    - 만약 `^python\s\w+` 라는 규칙이 있다면, 이는 문자열 전체에서 'python'으로 시작하면서 공백 한칸 뒤에 문자열이 오는 첫 번째 문장을 찾겠다는 의미이다.
    - 예를들어 10줄짜리 텍스트의 각 줄에 python one, python two, ... python ten 이 있다고 했을때, re.M 옵션 없이 매칭하면 문자열 전체에서 처음 등장한 'python one' 만을 매칭한다.
    - 하지만 문자열 전체가 아닌, 각각의 줄에서 첫 번째로 해당 규칙을 만족하는 문장을 찾고싶을수도 있다.
    - 이 때, re.M 옵션을 주면 python one, python two, ... python ten을 전부 매칭한다.
4. `re.X` 혹은 `re.VERBOSE`
    - 복잡한 정규식 표현을 작성할 때, 개행이나 공백을 넣어 가독성을 높일 수 있게 해준다.
    - 예를들어 `\s*GEOMFROMTEXT.+'\s*\)` 라는 규칙이 있다면, re.X 옵션을 주어 다음과 같이 표현할 수 있다.
    ```python
    re.comple("""
        \s*             # 처음 시작은 공백이 있을수도, 없을수도,
        GEOMFROMTEXT.+  # 그 후 'GEOMFROMTEXT' 뒤에 문자열이 따라오고,
        '\s*            # 따옴표 하나가 오고, 그 뒤에 공백이 있을수도, 없을수도
        \)              # 마지막은 닫힌 괄호로 끝난다.
    """, re.X)
    ```
    - 위 코드에서 `re.X` 옵션을 주지 않으면, 개행한 부분을 모두 하나의 규칙으로 인지하여 예측한 결과를 얻어낼 수 없다.
    - 또한, 각 규칙 부분마다 주석을 달 수 있으므로 규칙을 이해하는데도 용이하다.

<br/>

컴파일 옵션 `re.I` 를 통해 대소문자 구분없이 문자열을 매칭하는 방법을 알아보았다.

그리고 하는김에 그 외의 컴파일 옵션들에 대해서도 간략히 알아보았다.

각 컴파일 옵션에 대한 내용은 추후 좀 더 자세한 예제를 통해 따로 포스팅할 예정
