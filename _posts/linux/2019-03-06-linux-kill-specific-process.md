---
title: "[linux] 특정 이름이 들어간 프로세스 전부 종료하기"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 특정 이름을 가진 프로세스 죽이기

리눅스에서 특정 이름을 가진 프로세스를 죽이려면 다음과 같이 하면 된다.

```
ps -ef | grep itholic | awk '{print $2}' | xargs kill -9
```

'itholic' 이라는 이름을 가진 프로세스를 모두 찾아서 죽이는 명령이다.

`ps -ef | grep itholic` 까지만 입력하면, 'itholic' 이라는 이름을 가진 프로세스가 전부 출력된다.

`awk '{print $2}'` 는 앞 명령어의 결과 컬럼에서 두 번째 필드만 출력하는 명령이다.

참고로 ps -ef 명령의 두 번째 필드는 pid 이다.

즉, 'itholic' 이라는 이름을 가진 프로세스의 pid가 출력된다.

마지막으로 `xargs kill -9` 는, 앞에서 출력된 값을 인자로 `kill -9` 명령을 실행하라는 의미이다.

이 때 앞에서 전달받은 인자가 pid인데, kill명령으로 이를 모두 죽이는 것이다.

따라서 위 명령을 수행하면 최종적으로 'itholic'이라는 이름을 가진 프로세스가 전부 죽는 것이다.
