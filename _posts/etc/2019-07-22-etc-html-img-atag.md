---
title: "[html] 이미지에 링크걸기"
layout: post
tag:
- etc
- html
category: etc
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 이미지에 링크걸기

<br/>

다음과 같은 이미지가 있을 때,

해당 이미지를 클릭해 특정 링크로 이동하려면 어떻게 해야할까?

현재는 이미지를 클릭해도 아무일도 일어나지 않는다.

<img src="/assets/images/profile.jpg" width="200" align="left">

<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>

이미지에 링크를 걸기 위해서는 a 태그를 사용하면 된다.

html의 a 태그를 이용하면 다음과 같이 링크를 걸 수 있다.

```html
<a href="https://itholic.github.io/" target="_blank">
  <img src="이미지 경로" width="200" align="left">
</a>
```

이런식으로, 단순히 img 태그를 a 태그 안쪽으로 넣어주면 된다.

<br/>

이제 귀여운 몽실이 사진을 클릭하면 내 블로그 메인 화면으로 이동할 수 있게 되었다!

<a href="https://itholic.github.io/" target="_blank"><img src="/assets/images/profile.jpg" width="200" align="left"></a>

<br><br/>
<br><br/>
<br><br/>
<br><br/>

