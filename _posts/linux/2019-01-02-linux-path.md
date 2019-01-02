---
title: "[linux] 리눅스 PATH 설정"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스 PATH 설정

원하는 경로를 PATH에 추가하고싶으면 다음과 같이 하면 됨.

```
export PATH=$PATH:~/mypath/
```

PATH가 제대로 설정되었는지는 다음과 같이 확인.

```
echo $PATH
```

근데 이런식으로 export를 통해 환경변수를 추가하면, 재 로그인시 초기화된다.

영구적으로 적용하고싶다면 ~/.bashrc 혹은 ~/.bash_profile쪽에 아까 명령어로 입력한 내용을 추가하고 저장하면 된다.
