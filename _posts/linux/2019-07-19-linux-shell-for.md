---
title: "[linux][shell] 쉘 스크립트 for문 사용법"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 쉘 스크립트 for문 사용법

쉘 프로그래밍을 자주 하지는 않아서 관련 내용을 따로 정리하진 않았었는데,

오히려 가끔 사용하니까 할떄마다 찾아보게돼서 간단하게나마 정리를 하고자한다.

각설하고, 쉘 스크립트에서 for문은 다음과 같이 사용하면 된다.

```shell
  1 for num in 1 2 3 4 5
  2     do
  3         echo $num
  4     done
```

실행 결과는 (뻔하지만) 다음과 같다.

```
1
2
3
4
5
```

일반적인 for문이랑 형태는 크게 다르지 않은데,

특이했던 점은 우선 do 와 done을 사용해 for문의 범위를 정의해준다는 점이었고,

이터레이션할 리스트를 적어줄때 따로 콤마같은 구분자가 없이 그냥 띄어쓰기로 한다는 점.

(파이썬에 익숙해서 리스트라고 적긴 했는데, 쉘에선 '배열'이라는 표현이 더 통용되는 것 같은 느낌)

아, 그리고 선언한 변수를 출력할 때에는 앞에 달러표시($)를 써주어야 한다는 점이었다.

3번 라인에 $num이 아닌 그냥 num으로 쓰면 'num' 이라는 문자열 자체가 출력된다.

<br/>

이상, 매우 간단하게 쉘 스크립트 for문 사용법을 알아보겠다.

(사실 '쉘 스크립트 for문'이라기보다는 그냥 '쉘 for문'이 더 정확하긴 하지만, 어쨌든)