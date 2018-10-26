---
title: "[django] 장고 설치 with Virtualenv"
layout: post
tag:
- django
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# setup & runserver

장고 설치부터 웹 서버 띄우기까지의 간단한 튜토리얼

## 1. Virtualenv

한 서버에서 여러개의 프로젝트 진행 시, 여러 프로젝트의 파이썬 라이브러리 버전간 충돌을 방지하기 위해 프로젝트마다 독립적인 환경을 제공한다.

### 설치

```
pip install virtualenv
```

### 가상환경을 위한 디렉토리 생성

```
python -m virtualenv [디렉토리명]
```

### 가상환경 활성화

```
source [디렉토리명]/bin/activate
```
- 제대로 적용이 됐다면 콘솔입력창 앞에 (디렉토리명) 으로 접두어가 붙는다.


## 2. Django

python 기반의 웹 프레임워크이다. (가상환경이 활성화된 상태에서 진행해야 이후 다른 프로젝트 진행시 충돌을 방지할 수 있다)

### 설치

```
pip install django~=1.11.0
```

### Django 프로젝트 생성

```
django-admin startproject mydjango ./
```

- 제대로 생성되면 다음과 같은 구조이다.

```
./
|---manage.py
|---mydjango
    |---settings.py
    |---urls.py
    |---wsgi.py
    |---__init__.py
```

manage.py : 사이트를 관리하는 대부분의 명령을 지원
settings.py : 웹사이트 설정 관련 파일
urls.py : url 패턴정보 및 관련 정보 정의


### DB 생성

```
python manage.py migrate
```
- 웹 운영에 필요한 각종 DB 및 테이블 생성
- 새로운 앱이 추가되면 이 명령을 통해 DB를 만들어주어야함


### 서버 실행
```
python manage.py runserver 0.0.0.0:8000
```
- 뒤에 0.0.0.0을 붙여줘야 모든 호스트에서 접속 가능


### 접속 확인
```
브라우저에서 127.0.0.1:8000을 통해 접속
```




