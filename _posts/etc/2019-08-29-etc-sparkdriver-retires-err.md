---
title: "[spark] Service 'sparkDriver' failed after 16 retries (on a random free port)! 오류"
layout: post
tag:
- etc
- spark
category: etc
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0

---

# Spark Service 'sparkDriver' failed after 16 retries (on a random free port)! 오류 해결


MacOS에서 pyspark 사용중 다음과 같은 에러가 발생했다.

```
java.net.BindException: Can't assign requested address:
Service 'sparkDriver' failed after 16 retries (on a random free port)!
Consider explicitly setting the appropriate binding address for the service
'sparkDriver' (for example spark.driver.bindAddress for SparkDriver)
to the correct binding address.
```

`/etc/hosts` 파일에 local hostname을 추가해서 해결함

```
$ hostname
이 부분에 본인의 로컬 호스트 네임이 출력됨
```

`/etc/hosts` 파일을 열어서 위에서 출력된 이름을 다음과 같이 추가해준다.

```
127.0.0.1    HostName.local
127.0.0.1    localhost
```

localhost 는 이미 있을것이고,

이런식으로 `127.0.0.1` 에 본인의 로컬 호스트 네임을 명시적으로 바인딩해주면 된다.
