---
title: "[javascript] 화살표 표기법(arrow notation)"
layout: post
tag:
- javascript
- nodejs
category: javascript
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---


# javascript 화살표 표기법

javascript에서는 익명 함수를 사용할때 화살표 표기법이라는 녀석을 지원한다.

어떻게 쓰는지 직접 보자.

```javascript
const adder = function(a, b) {
    return a + b
}

console.log(adder(10, 20))
```

adder라는 변수에 익명함수를 할당했다.

인자로 전달받은 두 개의 값을 더해서 리턴해주는 간단한 함수이다.

실행하면 10과 20을 더한 값이 나온다.

```
30
```

위 코드를 화살표 표기법으로 바꾸면 다음과 같다.

```javascript
const adder = (a, b) => {
    return a + b
}

console.log(adder(10, 20))
```

function 키워드가 빠지고, 파라메터 선언부와 중괄호 사이에 화살표가 들어왔다.

더 간단히 표현할 수는 없을까?

```javascript
const adder = (a, b) => a + b

console.log(adder(10, 20))
```

정말로 작동할지 의구심이 들 정도로 훨씬 간결해졌다.

중괄호도 사라지고, return 키워드도 사라졌다.

실행해보자.

```
30
```

정상 동작한다.

이처럼 화살표 표기법을 적절히 활용하면 훨씬 간단 명료한 코딩이 가능해진다.
