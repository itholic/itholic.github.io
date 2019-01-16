---
title: "[linux] 리눅스 시스템 시간 확인 및 변경"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스 시스템 시간 변경

리눅스에서 시스템 시간을 확인하려면 다음과 같이 `date` 명령을 사용하면 된다.

```
$ date
Wed Jan 16 18:33:57 KST 2019
```

이를 바꾸고 싶다면 -s 옵션과 함께 다음과 같이 바꾸면 된다.

총 세 가지 방법이 있다.

```
$ date -s "13 JAN 2019 18:33:57"
$ date -s "2019-01-13 18:33:57"
$ date -s "20190113 18:33:57"
```

개인적으로 세 번째 방법이 제일 간단한 것 같다

시간만 변경하려면 앞부분을 제외하고 `18:33:57` 부분만 적어주면 된다.

한국 표준시간에 맞추고싶다면 타임서버를 활용하면 된다.

```
$ rdate -s time.bora.net
```

혹시 위 타임서버가 안되면 다음의 타임서버중 하나로 시도해보자.


- ntp.kornet.net
- ntp.postech.ac.kr
- time.nuri.net 
- time.windows.com


이 외에도 여러개의 타임 서버가 있으며,

타임 서버 목록은 <a href="https://zetawiki.com/wiki/%EA%B3%B5%EC%9A%A9_NTP_%EC%84%9C%EB%B2%84_%EB%AA%A9%EB%A1%9D" target="_blank">해당 링크</a> 에서 더 다양하게 살펴볼 수 있다.

참고로 rdate 명령이 없다고 나오면 yum을 통해 설치해주면 된다.

```
$ sudo yum install -y rdate
```

이상, 리눅스 시스템 시간 변경하는 방법을 알아보았다.
