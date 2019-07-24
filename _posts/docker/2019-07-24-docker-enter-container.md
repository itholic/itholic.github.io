---
title: "[Docker] 도커 컨테이너 접속 및 빠져나오기"
layout: post
tag:
- docker
category: docker
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 도커 컨테이너 접속 및 빠져나오기

<br/>

도커 이미지로부터 컨테이너를 실행시킨 후에,

컨테이너 안으로 들어가 뭔가 작업을 하고싶을때가 있다.

그리고 작업을 하다가 다시 밖으로 빠져나오고 싶을수도 있다.

알아보자.

<br/>

### 1. 실행중인 컨테이너 목록 확인

```shell
$ docker ps
CONTAINER ID    IMAGE      COMMAND      CREATED       STATUS       PORTS     NAMES
134adb2ba12     my-image   "/bon/bash"  2 hours ago   Up 2 hours             my-container
```

위와 같이 목록이 출력되면,

접속하고자 하는 컨테이너의 'CONTAINER ID' 또는 'NAMES' 정보를 활용해 다음 명령을 입력하면 된다.

<br/>

### 2. 컨테이너 접속

<br/>

CONTAINER ID 혹은 NAMES를 활용해 접속해보자.

```shell
$ docker exec -it [134adb2ba12 혹은 my-container] /bin/bash
root@134adb2ba12:~/$ 
```

위와 같이 쉘 프롬프트에 CONTAINER ID가 뜨면서 모양이 바뀌면 접속 성공이다.

이제 컨테이너 안쪽에서 마음껏 원하는 작업을 수행하면 된다.

<br/>

exec 명령은 도커 컨테이너 안쪽에 명령어를 전송할때 사용한다.

이 때, 명령어를 `/bin/bash` 로 주게되면 도커 컨테이너 안쪽의 bash 쉘이 실행된다.

접속이란게 결국 리눅스의 쉘을 사용하겠다는 뜻이기 때문에, 이런 방식으로 컨테이너에 접속한다.

<br/>

참고로 -i 옵션은 표준 입출력을 사용하겠다는 의미로,

-t 옵션만 주게되면 `root@134adb2ba12:~/$` 와 같이 프롬프트 모양이 바뀌긴 한다.

하지만 표준 입출력 옵션을 주지 않았으므로 입력을해도 아무런 반응이 없다.

<br/>

또한 -t 옵션은 가상 tty를 통해 접속하겠다는 의미로,

-i 옵션만 주게되면 `root@134adb2ba12:~/$` 부분이 뜨지 않는다.

그냥 빈 입력화면이 나오는데, 다만 명령어를 입력하면 명령은 제대로 수행된다.

<br/>

### 3. 컨테이너 빠져나오기

<br/>

컨테이너를 빠져나올때는 단순히 exit 명령을 사용하면 된다.

```shell
$ docker exec -it [134adb2ba12 혹은 my-container] /bin/bash
root@134adb2ba12:~/$
root@134adb2ba12:~/$ exit
$
```

이상,

도커 컨테이너에 접속하는 방법과,

다시 빠져나오는 방법을 간단히 알아보았다.
