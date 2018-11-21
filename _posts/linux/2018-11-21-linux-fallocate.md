---
title: "[linux] 리눅스 대용량 파일 만들기 (fallocate)"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스 대용량 파일 만들기

가끔 테스트를 위해 특정 용량의 파일이 필요할때가 있다.

일일이 내용을 채워넣자니 정확한 용량을 맞추기가 번거롭다.

이런 상황에서 손쉽게 테스트용 파일을 만들 수 있도록 도와주는 명령어가 있다.

바로 fallocate 명령어다.

```
[itholic@linux test]$ fallocate -l 10 testfile
```

위 명령은 testfile이라는 이름의 10byte짜리 파일을 생성한다.

용량을 확인해보자.

```
[itholic@linux test]$ ls -lh testfile
-rw-r--r--. 1 itholic itholic 10 2018-11-21 07:42 testfile
```

10바이트짜리 파일이 생성된 것을 확인할 수 있다.

cat으로 내용을 보면 아무것도 나오지 않고, 

파일을 직접 열어보면 알 수 없는 문자열로 가득 채워져있다.

<br/>

숫자 뒤에 키워드를 주어, 다음과 같이 용량을 손쉽게 할당 가능하다.

```
[itholic@linux test]$ fallocate -l 10K testfile_10kb
[itholic@linux test]$ fallocate -l 10M testfile_10mb
[itholic@linux test]$ fallocate -l 10G testfile_10gb
[itholic@linux test]$ ls -lh
합계 11G
-rw-r--r--. 1 itholic itholic 10G 2018-11-21 07:52 testfile_10gb
-rw-r--r--. 1 itholic itholic 10K 2018-11-21 07:52 testfile_10kb
-rw-r--r--. 1 itholic itholic 10M 2018-11-21 07:52 testfile_10mb
```

K, M, G 키워드를 주어 각각 KB, MB, GB 급의 파일을 손쉽게 생성했다.
