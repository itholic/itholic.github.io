---
title: "[linux][basic] rm - 파일, 디렉토리(폴더) 삭제"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# rm (remove)

리눅스에서 파일을 삭제하려면 `rm` 명령어를 사용하면 된다.

```
$ rm [삭제할 파일 경로]
```

`origin` 이라는 파일이 있다고 가정하고, 이를 삭제해보자.

```
$ rm origin
```

디렉토리(폴더)를 삭제할 때에는 -r 옵션을 추가해주면 된다.

`origin_dir`이라는 디렉토리를 삭제해보자.

```
$ rm -r origin_dir
```
