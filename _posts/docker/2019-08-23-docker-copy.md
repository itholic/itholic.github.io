---
title: "[Docker] 도커 파일 복사 (로컬 <-> 컨테이너)"
layout: post
tag:
- docker
category: docker
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 도커 파일 복사

<br/>

도커 컨테이너 안에 있는 파일을 로컬로 복사하는 방법과

로컬의 파일을 컨테이너로 복사하는 명령어를 간단히 알아보자.

docker cp 라는 명령어로 간단히 가능하다.

<br/>

## 1. 컨테이너 안에 있는 파일을 로컬로 복사

<br/>

"tmp_container"라는 컨테이너 내부에 "/root/data/test.md" 라는 파일이 있다고 하자.

이 파일을 로컬(호스트)의 "~/data/" 위치로 가져오려면 다음과 같이 하면 된다.

```shell
$ docker cp tmp_container:/root/data/test.md ~/data/ 
```

cp 명령어 뒤에 컨테이너 이름과 컨테이너 내부 데이터 경로를 ":" 로 구분해 적어준다.

그 뒤에는 데이터를 복사해올 로컬 경로를 적어주면 된다.

<br/>

## 2. 로컬의 파일을 컨테이너 안으로 복사

이번엔 로컬의 "~/data/test.md" 라는 파일을 컨테이너의 "/root/data/"로 복사해보자.

그냥 명령 인자의 순서를 반대로 해주면 된다.

```shell
$ docker cp ~/data/test.md tmp_container:/root/data/
```
