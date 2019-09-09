---
title: "[git] diff로 브랜치간 차이점 확인하기"
layout: post
tag:
- git
category: git
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# git diff 브랜치

git diff로 브랜치간 차이를 알아보는 방법은 간단하다.

diff 명령의 인자로 비교를 원하는 두 개의 브랜치를 넣어주면 된다.

```shell
$ git diff origin/master origin/my_branch
```

위 명령은 master브랜치와 my\_branch의 차이를 보여준다.
