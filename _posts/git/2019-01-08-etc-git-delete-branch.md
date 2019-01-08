---
title: "git 브랜치 삭제 (git delete branch)"
layout: post
tag:
- etc
- git
category: etc
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# git branch delete(remove)

git 에서 브랜치를 삭제하는 방법은 두 가지다.

삭제할 브랜치명은 'sample-branch'라고 하자.

1. 본인의 로컬 환경에서만 삭제하는법

```
git branch -D sample-branch
혹은
git branch --delete sample-branch
```

2. 원격지 브랜치를 삭제하는법 (원본을 날리는 행위이므로 신중하게 사용하자)

```
git push origin :sample-branch
```
