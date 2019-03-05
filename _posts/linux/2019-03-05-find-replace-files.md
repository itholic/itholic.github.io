---
title: "[linux] 여러 파일의 문자열 찾아 바꾸기"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스에서 여러 파일내 문자열 치환하기

특정 파일에서 'hello'라는 문자열을 'bye'로 바꾸려면,

vi로 파일을 열고 command 모드에서 다음과 같이 명령하면 된다.

(command모드는 사용자가 콜론(:)을 입력해 맨 아래쪽에 콜론이 떠있는 상태를 말한다)

```
:s/hello/bye/g
```

아주 간단하다.

그런데 이러한 명령을 수천, 수만개의 파일에서 수행해야 한다면 어떨까?

다음과 같이 리눅스 쉘에서 find명령어를 적절히(;) 활용하면 된다.

```
find . -name "*.sh" -exec perl -pi -e 's/hello/bye/g' {} \;
```

현재 경로 이하에 있는 모든 디렉토리에서,

'sh' 라는 확장자를 가진 모든 파일에 대하여,

`'s/hello/bye/g'` 명령을 수행하라는 명령어이다.

물론 문자열 치환 뿐만 아니라 해당 부분의 명령어를 바꾸면 어떤 명령이든 수행 가능하다.
