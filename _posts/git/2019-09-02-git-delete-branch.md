---
title: "[git] 브랜치 삭제(delete branch)"
layout: post
tag:
- git
category: git
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# git 브랜치 삭제

`my_branch` 라는 브랜치를 삭제

```
$ git branch -D my_branch
```

-D 대신 --delete 옵션도 동일하게 동작

현재는 로컬에서만 삭제된 상태

리모트 브랜치에도 적용하기 위해서는 다음 명령 입력

```
$ git push origin :my_branch
```
