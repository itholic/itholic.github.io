---
title: "[linux][basic] cp - 파일, 디렉토리(폴더) 복사"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# cp (copy)

리눅스에서 파일을 복사하려면 `cp` 명령어를 사용하면 된다.

```
$ cp [원본 경로] [복사본 경로]
```

`origin` 이라는 파일이 있다고 가정하고, 이를 복사해 `target`이라는 파일을 생성해보자.

```
$ cp origin target
```

이는 동일한 디렉토리에 복사본을 생성한 것이고,

만약 다른 디렉토리로 복사하고 싶다면, 해당 경로를 함께 적어주면 된다.

```
$ cp origin ~/data/target
```

`~/data` 디렉토리 밑으로 `target` 이라는 이름의 복제본을 만들었다.

참고로 `~/` 는 유저의 홈 디렉토리를 의미한다.

유저가 `itholic`이라면, 위 명령어는 다음과 같다.

```
$ cp origin /home/itholic/data/target
```

만약 복제본의 이름을 지정하지 않고 목적 경로만 적어주면,

목적 경로에 원본 파일과 똑같은 이름으로 복제본이 생성된다.

```
$ cp origin ~/data/
```

위 명령을 수행하면 `~/data/` 경로에 `origin` 이라는 이름으로 사본이 생성된다.

디렉토리(폴더)를 복사할 때에는 -r 옵션을 추가해주면 된다.

`origin_dir`이라는 디렉토리를 복사해서 `target_dir` 디렉토리를 생성해보자.

```
$ cp -r origin_dir target_dir
or
$ cp -r origin_dir ~/data/target_dir
or
$ cp -r origin_dir ~/data/
```
