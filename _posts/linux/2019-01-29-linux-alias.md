---
title: "[linux] 리눅스 alias로 명령어 변수화하기"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# alias

alias는 특정 명령어를 본인이 원하는 형태로 사용할 수 있도록 변수화하는 기능이다.

alias라는 이름 그대로 특정 명령에 '별칭'을 주는 것이다.

<br/>

예를들어 리눅스에서 `ls` 명령을 사용할때, 거의 모든 상황에서 `-alh` 옵션을 주어 사용한다고 가정하자.

그렇다면 매번 `ls -alh` 를 타이핑 하기보다는 `lsa` 라는 명령어 별칭을 만들거나, 혹은 그냥 `ls` 자체를 `ls -alh`와 동일하게 동작하도록 하는게 편하지 않을까?

다음과 같이 해주면 된다.

```
$ alias lsa='ls -alh'
```

변수를 할당하듯이 우선 좌측에 alias이름을 적어주고, 우측에 실제로 동작하기를 원하는 명령을 따옴표 안에 적어주면 된다 (큰따옴표도 가능)

그 후 alias로 설정한 `lsa` 명령을 입력하면, alias로 등록한 `ls -alh`가 동작하는 것을 확인할 수 있다.

```
$ lsa
total 120
drwxr-xr-x  13 itholic  itholic   416B  1 29 09:20 .
drwxr-xr-x  15 itholic  itholic   480B  1 23 10:20 ..
-rw-r--r--   1 itholic  itholic   5.3K  1 22 17:18 2018-10-25-linux-cd.md
-rw-r--r--   1 itholic  itholic   5.1K  1 22 17:18 2018-10-26-linux-chmod.md
-rw-r--r--   1 itholic  itholic   3.9K  1 22 17:18 2018-11-01-linux-top.md
-rw-r--r--   1 itholic  itholic   8.4K  1 22 17:18 2018-11-06-linux-basic-command.md
-rw-r--r--   1 itholic  itholic   1.6K  1 22 17:18 2018-11-21-linux-fallocate.md
-rw-r--r--   1 itholic  itholic   3.9K  1 22 17:18 2018-11-22-linux-split.md
-rw-r--r--   1 itholic  itholic   3.1K  1 22 17:18 2018-11-23-history.md
-rw-r--r--   1 itholic  itholic   4.0K  1 22 17:18 2018-11-24-find-rm.md
-rw-r--r--   1 itholic  itholic   635B  1 22 17:18 2019-01-02-linux-path.md
-rw-r--r--   1 itholic  itholic   1.4K  1 22 17:18 2019-01-16-linux-date.md
-rw-r--r--   1 itholic  itholic   1.1K  1 29 09:20 2019-01-29-linux-alias.md
```

설정한 alias 목록을 확인하려면 단순히 `alias` 만 입력해주면 된다.

```
$ alias
alias lsa='ls -alh'
```

alias를 설정할때 입력한 명령어 리스트가 출력된다.

마지막으로 설정한 alias를 해제하려면 간단하게 unalias 명령을 사용하면 된다.

```
$ unalias lsa
```

이 외에도 특정 경로로 이동하는 명령어, 특정 프로세스를 찾아 없애는 명령어 등 자주 사용하는 명령어를 alias로 등록하면 보다 쾌적한 리눅스 라이프(?)를 영위할 수 있다.

참고로 vim 에디터를 열때 단순히 'vi' 만 입력해도 자동으로 vim에디터가 열리도록 하는 `alias vi='vim'` 이 대표적인 사용 예이다.
