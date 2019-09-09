---
title: "[python] requirements.txt로 패키지 관리하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# requirements.txt로 패키지 한 방에 관리하기

파이썬으로 프로젝트를 진행하게되면 pip으로 여러 패키지를 설치하게된다.

pip list를 입력하면 다음과 같이 pip으로 설치된 모든 패키지가 나온다.

```shell
$ pip list
Package                       Version
----------------------------- -----------
alabaster                     0.7.12
alembic                       1.0.11
appnope                       0.1.0
atomicwrites                  1.3.0
attrs                         19.1.0
Babel                         2.7.0
backcall                      0.1.0
...
idna                          2.8
imagesize                     1.1.0
importlib-metadata            0.19
ipykernel                     5.1.2
ipython                       7.7.0
ipython-genutils              0.2.0
ipywidgets                    7.5.1
itsdangerous                  1.1.0
jdcal                         1.4.1
```

너무 많아서 중간에 생략했다.

어쨌든 이 패키지들을 그대로 다른 환경에서 설치하고 싶을땐 어떻게하면 좋을까?

일일이 손으로 타이핑하기엔 너무 귀찮을 것 같다.

requirements.txt는 이러한 패키지 목록이 나열되어있는 텍스트 파일이다.

이름은 꼭 requirements.txt로 할 필요는 없는데,

대부분 프로젝트에서 requirements.txt라는 이름으로 관리하고 있으니 웬만하면 맞춰주는 것이 좋다.

다음 명령으로 손쉽게 requirements.txt 생성이 가능하다.

```shell
$ pip freeze > requirements.txt
```

파일을 열어보면 다음과 같이 버전 정보까지 알아서 정리해준다.

```
alabaster==0.7.12
alembic==1.0.11
appnope==0.1.0
atomicwrites==1.3.0
attrs==19.1.0
Babel==2.7.0
backcall==0.1.0
...
idna==2.8
imagesize==1.1.0
importlib-metadata==0.19
ipykernel==5.1.2
ipython==7.7.0
ipython-genutils==0.2.0
ipywidgets==7.5.1
itsdangerous==1.1.0
jdcal==1.4.1
```

역시 너무 길어서 중간은 `...` 으로 생략했다.

이제 다음 명령을 실행하면 모든 패키지를 한 번에 설치해준다.

```shell
$ pip install -r requirements.txt
```

pip install에 -r 옵션과 함께 패키지 목록이 적힌 파일명을 인자로 주면 된다.

끝!

<br/>

+

참고로 `inda==2.8` 같은 경우, idna라는 패키지를 정확히 2.8 버전으로 설치한다는 뜻이다.

하지만 정확히 2.8 버전이 아닌, 단순히 해당 버전 이상을 설치하고싶을수 있다.

이럴땐 다음과 같이 해주면 되고,

```
idna>=2.8
```

만약 2버전대의 아무 버전이나 설치하고싶다면 다음과 같이 해주면 된다.

```
idna>=2.*
```

이 외에도 지원하는 표현 방식은 다양하게 있으니, 필요에따라 찾아서 사용하면 된다.
