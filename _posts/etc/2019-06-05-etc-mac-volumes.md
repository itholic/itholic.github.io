---
title: "맥북(MacOS) USB/외장하드 경로"
layout: post
tag:
- etc
category: etc
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 맥북에서 USB, 외장하드 경로

<br/>

우선 결론부터 말하면 맥북에 연결된 외부 장치의 경로는 모두 /volumes/ 아래 존재한다.

아래는 좀 더 자세한 설명이다.

<br/>

윈도우즈에서는 USB나 외장하드를 연결시켰을때,

그 경로를 알아내는것이 어렵지 않다.

다음과 같이 내컴퓨터에서 해당 장치를 찾은 후, 주소창을 확인하면 된다.

![windows](/assets/images/2019/06/05/etc-mac-volumes/windows.png)

<br/>

하지만 맥북이나 미니맥같은 MacOS에서 외부장치를 연결하면,

다음과 같이 화면에 디스크 아이콘이 뜨기때문에 마치 ~/Desktop/ 경로에 있는 것처럼 보인다.

![desktop](/assets/images/2019/06/05/etc-mac-volumes/desktop.png)

<br/>

하지만 터미널에서 Desktop 경로를 뒤져보면 외부장치경로를 찾을 수 없다고 나온다.

![nosuchfile](/assets/images/2019/06/05/etc-mac-volumes/nosuchfile.png)

<br/>

맥북에서 외장하드 위치는 다음과 같이 /volumes/ 경로에 존재한다.

![volumes](/assets/images/2019/06/05/etc-mac-volumes/volumes.png)

<br/>

이상, 맥북(MacOS)에서 연결된 외부기기의 경로에대해 간단히 알아보았다.