---
title: "[git] 파일 수정 내용 취소하기 (변경내용 되돌리기)"
layout: post
tag:
- git
category: git
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# git 파일 변경내용 원래대로 되돌리기

<br/>

git에서 작업 내용을 되돌리는 방법은 두 가지가 있다.

모든 변경 사항을 초기화하는 방법과,

특정 파일의 변경 사항만 초기화하는 방법이다.

<br/>

1. 모든 파일에 대한 변경을 초기 상태로 되돌리기

모든 파일을 작업 이전의 상태로 돌리며, 되돌릴수 없으므로 주의

```shell
$ git reset --hard
```

<br/>

2. 특정 파일에 대한 변경만 되돌리기

```shell
$ git checkout -- <파일명>
```


