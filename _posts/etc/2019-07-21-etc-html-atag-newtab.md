---
title: "[html] a 태그 클릭시 새 창으로 열기"
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

# a 태그 새 창으로 열기

html의 a 태그를 이용하면 특정 페이지에 대한 링크를 걸 수 있다.

```html
<a href="https://itholic.github.io/">코딩장이 블로그</a>
```

다음과 같이 링크가 생성되는데,

클릭하면 이 창에서 빠져나가게 된다.

<a href="https://itholic.github.io/">코딩장이 블로그</a> (현재 창에서 실행됨)

<br/>

해당 페이지를 그대로 놔두고 새 창에서 띄우려면,

다음과 같이 target 옵션을 `_blank` 로 지정하면 된다.

```html
<a href="https://itholic.github.io/" target="_blank">코딩장이 블로그</a>
```

아래 링크는 그냥 보기엔 위의 링크랑 똑같지만,

클릭해보면 새 창에서 실행되는 것을 확인할 수 있다.

<a href="https://itholic.github.io/" target="_blank">코딩장이 블로그</a> (새 창에서 실행됨)
