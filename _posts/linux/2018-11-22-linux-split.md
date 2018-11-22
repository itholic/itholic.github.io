---
title: "[linux] 리눅스 파일 분할 (split)"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스 대용량 파일 분할하기

용량이 큰 데이터를 다루다보면 파일들을 적절한 용량으로 쪼개서 처리해야하는 경우가 있다.

예를들어 10GB짜리 csv파일을 DB에 밀어넣어야 하는 경우,

1GB짜리 파일 10개로 나누어서 분산처리하는것이 통째로 넣는것보다 성능상 이득인 경우가 있다.

우선 이전에 포스팅했던 <a href="https://itholic.github.io/linux-fallocate/" target="_blank">fallocate 명령어</a>로 10GB짜리 파일을 만들어보자.

```
[itholic@linux test]$ fallocate -l 10G testfile_10gb
[itholic@linux test]$ ls -lh
합계 11G
-rw-r--r--. 1 itholic itholic 10G 2018-11-22 01:27 testfile_10gb
```

파일이 생성되었다. 

이제 1GB 단위로 쪼개보자.

split명령어를 사용하면 다음과 같이 간단하게 파일 분할이 가능하다.

```
[itholic@linux test]$ split -b 1G 
[itholic@linux test]$ ls -lh
합계 20G
-rw-r--r--. 1 itholic itholic  10G 11월 22 10:37 testfile_10gb
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xaa
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xab
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xac
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xad
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xae
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xaf
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xag
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xah
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xai
-rw-rw-r--. 1 itholic itholic 1.0G 11월 22 10:38 xaj
```

파일이 잘 분할되었다.

또한, 라인 단위로 파일을 나눌수도 있다.

다음과 같이 임의의 10000줄짜리 파일을 생성했다.

```
    1 let's split the file line by line
    2 let's split the file line by line
    3 let's split the file line by line
    4 let's split the file line by line
    5 let's split the file line by line
    6 let's split the file line by line
    7 let's split the file line by line

             ... 
             ...

 9994 let's split the file line by line
 9995 let's split the file line by line
 9996 let's split the file line by line
 9997 let's split the file line by line
 9998 let's split the file line by line
 9999 let's split the file line by line
10000 let's split the file line by line
```

파일의 길이는 다음과 같이 wc -l 명령을 활용해 쉽게 구할수도 있다.

```
[itholic@linux test]$ cat testfile_10000line | wc -l
10000
```

이제 이 파일을 100줄짜리 파일 100개로 나누어보자.

```
[itholic@linux test]$ split -l 100 testfile_10000line
[itholic@linux test]$ ls
testfile_10000line  xae  xaj  xao  xat  xay  xbd  xbi  xbn  xbs  xbx  xcc  xch  xcm  xcr  xcw  xdb  xdg  xdl  xdq  xdv
xaa                 xaf  xak  xap  xau  xaz  xbe  xbj  xbo  xbt  xby  xcd  xci  xcn  xcs  xcx  xdc  xdh  xdm  xdr
xab                 xag  xal  xaq  xav  xba  xbf  xbk  xbp  xbu  xbz  xce  xcj  xco  xct  xcy  xdd  xdi  xdn  xds
xac                 xah  xam  xar  xaw  xbb  xbg  xbl  xbq  xbv  xca  xcf  xck  xcp  xcu  xcz  xde  xdj  xdo  xdt
xad                 xai  xan  xas  xax  xbc  xbh  xbm  xbr  xbw  xcb  xcg  xcl  xcq  xcv  xda  xdf  xdk  xdp  xdu
```

100개의 파일로 나누어졌다.

특정 디렉토리 내에 파일 갯수를 확인하려면 다음과 같이 명령하면 된다.

```
[itholic@linux test]$ find . -type f | wc -l
101
```

현재 디렉토리에서 type이 파일타입의 데이터를 찾아서(디렉토리는 제외) 갯수를 확인하는 예제이다.

총 101개, 즉, 원본을 제외한 100개의 분할본이 잘 생성된것을 확인할 수 있다.

분할본의 라인이 100줄씩 잘 나누어졌는지 확인해보자.

```
[itholic@linux test]$ cat xaa | wc -l
100
[itholic@linux test]$ cat xab | wc -l
100
[itholic@linux test]$ cat xac | wc -l
100
```

잘 나누어졌다.
