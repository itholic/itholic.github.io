---
title: "[python] 특정 파일 리스트 가져오기(listdir, glob) "
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 특정 폴더(디렉토리) 파일 리스트 가져오기

코딩을 하다보면 특정 폴더에 있는 특정 파일 리스트를 가져와서 사용해야하는 경우가 있다.

이는 os 모듈 혹은 glob 모듈을 사용해서 해결할 수 있다.

## os.listdir

우선 os 모듈의 listdir을 사용해 특정 폴더에 있는 .py 파일만 가져와보자.

```python
# -*- coding: utf-8 -*-

import os

path = "./"
file_list = os.listdir(path)

print ("file_list: {}".format(file_list))
```

코드는 매우 간단하다.

현재 디렉토리에 있는 모든 파일(디렉토리) 리스트를 가져온다.

실행 결과는 다음과 같다.

```
file_list: ['testdira', 'eq.js', 'test.db', 'etl.py', '.etl.py.swp', 'testdirb', 'testdirc', 'find_file.py', 'asd.py', 'namespace_.py', 'namespace_2.py', 'eq.py']
```

디렉토리 내에 있는 모든 파일 및 디렉토리 리스트가 나왔다.

내가 원하는 파일은 .py 확장자를 가진 파일이므로, 코드를 추가해보자.

```python
# -*- coding: utf-8 -*-

import os

path = "./"
file_list = os.listdir(path)
file_list_py = [file for file in file_list if file.endswith(".py")]

print ("file_list_py: {}".format(file_list_py))
```


file_list에서 파일명이 .py로 끝나는 데이터만 file_list_py에 다시 정의했다.

실행해보자.

```
file_list_py: ['etl.py', 'find_file.py', 'asd.py', 'namespace_.py', 'namespace_2.py', 'eq.py']
```

확장자가 py인 파일만 정상적으로 추출해냈다.

# glob.glob

이번엔 glob을 써보자.

```python
# -*- coding: utf-8 -*-

import glob

path = "./*"
file_list = glob.glob(path)
file_list_py = [file for file in file_list if file.endswith(".py")]

print ("file_list_py: {}".format(file_list_py))
```

os.listdir과 완전히 같은 형태인데,

자세히보면 path를 정의하는 부분에 애스터리스크(*)가 붙은것이 보인다.

실행해보자.

```
file_list_py: ['./etl.py', './find_file.py', './asd.py', './namespace_.py', './namespace_2.py', './eq.py']
```

원하는 파일 목록을 잘 추출했다.

## 차이점

얼핏보면 os.listdir과 glob.glob은 똑같아 보이지만 약간 다르다.

비교해보자.


1. os.listdir을 사용했을 경우
```
file_list: ['testdira', 'eq.js', 'test.db', 'etl.py', '.etl.py.swp', 'testdirb', 'testdirc', 'find_file.py', 'asd.py', 'namespace_.py', 'namespace_2.py', 'eq.py']
```

2. glob.glob을 사용했을 경우
```
file_list: ['./testdira', './eq.js', './test.db', './etl.py', './testdirb', './testdirc', './find_file.py', './asd.py', './namespace_.py', './namespace_2.py', './eq.py']
```

차이점이 보이는가?

os.listdir을 사용한 경우는 해당 디렉토리의 파일명만 가져왔지만,

glob으로 파일 리스트를 가져올 경우에는 검색시 사용했던 경로명까지 전부 가져온다.

예를들어 현재 경로가 아닌 특정 경로의 파일을 찾는다면 다음과 같은 차이가 보일것이다.

1. os.listdir을 사용했을 경우 (./test/ 경로의 파일 검색)
```
file_list: ['testdira', 'eq.js', 'test.db', 'etl.py', '.etl.py.swp', 'testdirb', 'testdirc', 'find_file.py', 'asd.py', 'namespace_.py', 'namespace_2.py', 'eq.py']
```

2. glob.glob을 사용했을 경우 (./test/ 경로의 파일 검색)
```
file_list: ['./test/testdira', './test/eq.js', './test/test.db', './test/etl.py', './test/testdirb', './test/testdirc', './test/find_file.py', './test/asd.py', './test/namespace_.py', './test/namespace_2.py', './test/eq.py']
```

조금 더 차이가 와닿는다.

listdir은 해당 경로의 파일/디렉토리명만 가져오지만,

glob의 경우는 탐색한 경로까지 함께 가져온다.

당장은 별거 아닌것처럼 보이지만 상황에 따라ㅇ 차이가 될 수도 있을 것 같다.

차이점을 잘 이해해서 효율적인 코딩을 하자!