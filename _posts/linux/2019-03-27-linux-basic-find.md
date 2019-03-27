---
title: "[linux][basic] find - 특정 이름을 가진 파일 찾기"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# find

리눅스에서 특정 이름을 가진 파일을 찾고싶을때 find 명령을 사용할 수 있다.

예를들어 현재 위치를 기준으로 하위 모든 경로에서 .txt 로 끝나는 파일을 찾고싶다면?

```
$ find ./ -name '*.txt'
```

find 명령어 바로 뒤에는 파일을 찾고자하는 경로를 적어주면 된다.

예를들어 `/home/hjlee/data/` 라는 디렉토리를 밑에 있는 경로를 모두 찾으려면 이렇게 하면 될 것이다.

```
$ find /home/hjlee/data/ -name '*.txt'
```

그 뒤에 따라오는 -name은, 특정 이름을 기준으로 파일을 찾겠다는 옵션이다.

그리고 마지막으로 찾고자하는 파일의 이름 규칙을 적어주면 된다.

`*` 은 모든 문자열을 의미한다.

실제로 `'*'` 이라는 문자열이 포함된 파일명을 찾으려면 역슬래시 `(\)`를 통해 escape해주면 된다.

```
$ find /home/hjlee/data/ -name '*\*.txt'
```

예를들어 위 명령은 `/home/hjlee/data/` 의 하위 경로에서 다음과 같은 파일들을 찾아낼 것이다.

```
hello*.txt    asd*.txt    *.txt    ***.txt
```

<br/>

find 명령은 특정 이름 뿐만 아니라 여러 조건으로 파일을 검색할 수 있다.

특정 용량을 기준으로 검색을 한다던지,

변경된 시점을 기준으로 검색을 한다던지,

특정 권한을 기준으로 검색을 한다던지...

등등 여러가지 옵션이 존재한다.


