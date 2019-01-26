---
title: "[linux] vi 문자열 바꾸기"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# vi 문자열 바꾸기

다음과 같은 파일이 있을때,

파일에 포함된 모든 'bye' 를 'hello'로 바꾸어보자.

```
bye world, bye itholic
bye python
bye java
bye c++ 
```

vi의 콜론모드에서 다음과 같이 입력하면 된다.

```
:%s/bye/hello
```

%s 명령어 뒤에 슬래쉬(/)로 명령어를 구분해주고,

찾을 문자열, 변경할 문자열을 차례로 입력해주면 된다.

위 명령을 실행하면, 다음과 같이 변경된다.

```
hello world, bye itholic
hello python
hello java
hello c++
```

자세히보니 첫 번째 줄의 bye가 하나 변경되지 않았다.

이처럼 아무런 옵션 없이 실행하게되면 각줄에서 첫 번째로 찾아낸 문자열에 대해서만 변환을 수행한다.

모든 문자열을 변경하려면 다음과 같이 g 옵션을 주면 된다.

```
:%s/bye/hello/g
```

만약 각 줄의 맨뒤에 느낌표(!)를 추가하고 싶다면 어떻게 하면 될까?

각 줄의 맨 끝을 의미하는 $ 기호를 활용하면 된다.

```
:%s/$/!
```

다음과 같이 각 줄의 맨 끝에 느낌표가 붙은것을 확인할 수 있다.

```
hello world, hello itholic!
hello python!
hello java!
hello c++!
```
