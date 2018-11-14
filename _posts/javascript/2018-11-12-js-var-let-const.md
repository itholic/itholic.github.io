---
title: "[javascript] var, const, let 차이"
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

# var, const, let

javascript에서 변수는 var, const, let 세 개의 키워드로 정의 가능하다.

우선 var와 const의 차이는 다음과 같다.

```js
// var.js
  1 var a = 10
  2 a = 11
```

위와 같이 var의 경우 변수를 할당하고 값을 바꿀 수 있다.

```js
// const.js
  1 const A = 10
  2 A = 11
```

하지만 const는 값을 바꾸려고 하면 다음과 같은 에러가 발생한다.

```
A = 11
  ^

TypeError: Assignment to constant variable.
    at Object.<anonymous> (/home/iris/nodetest/var.js:2:3)
    at Module._compile (internal/modules/cjs/loader.js:688:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:699:10)
    at Module.load (internal/modules/cjs/loader.js:598:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:537:12)
    at Function.Module._load (internal/modules/cjs/loader.js:529:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:741:12)
    at startup (internal/bootstrap/node.js:285:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:739:3)
```

이미 이름만 보고 짐작했을 수도 있지만, const는 상수이다.

그래서 한 번 지정한 값을 바꾸려고 하면 에러가 나는 것이다.

그럼 let은 어떨까?

```js
// let.js
  1 let a = 10
  2 a = 10
```

위 코드를 실행하면 var와 같이 에러가 나지 않는다.

그럼 일단 값을 변경할 수 있다는 점에서 const와의 차이는 명확히 알 것 같다.

그렇다면 let과 var의 차이는 무엇일까?

```js
// var_hoisting.js
  1 console.log(a)
  2 var a = 10
```

위 코드를 실행하면 `undefined`가 출력된다.

이는 변수 <a href="https://itholic.github.io/js-hoisting/" target="_blank">호이스팅</a>에 의해 var a 의 선언부가 위쪽으로 끌어 당겨져 발생하는 현상이다.

그럼 let은 어떨까?

```js
// let_hoisting.js
  1 console.log(a)
  2 let a = 10
```

위 코드를 실행하면 다음과 같은 에러가 발생한다.

```
(function (exports, require, module, __filename, __dirname) { console.log(a)
                                                                          ^

ReferenceError: a is not defined
    at Object.<anonymous> (/home/iris/nodetest/var.js:1:75)
    at Module._compile (internal/modules/cjs/loader.js:688:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:699:10)
    at Module.load (internal/modules/cjs/loader.js:598:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:537:12)
    at Function.Module._load (internal/modules/cjs/loader.js:529:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:741:12)
    at startup (internal/bootstrap/node.js:285:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:739:3)
```

a가 아직 선언되지 않았다는 에러이다.

즉, 변수 호이스팅이 발생하지 않았다.

그럼 const의 경우는 어떨까?

```js
// const_hoisting.js
  1 console.log(a)
  2 const a = 10
```

위 코드를 실행하면 let의 경우와 완전히 동일한 에러가 출력된다.

여기까지 간단히 var, const, let의 차이를 정리하자면 다음과 같다.

```
var   : 값 변경 O, 호이스팅 O
let   : 값 변경 O, 호이스팅 X
const : 값 변경 X, 호이스팅 X
```

호이스팅은 예기지 못한 에러를 발생할 수 있으므로,

일반적으로 변수를 선언할때 let이나 const를 권유한다고 한다.

<br/>

마지막으로 재선언 가능 여부를 알아보자.

결론부터 말하면 재선언은 var만 가능하다.

```js
var a = 10
var a = 20
```

위 코드는 에러가 나지 않지만, 다음 두 개의 코드는 모두 에러가 난다.

```js
let a = 10
let a = 20  // SyntaxError: Identifier 'b' has already been declared
```

```js
const a = 10
const a = 20  // SyntaxError: Identifier 'c' has already been declared
```

최종적으로 var, let, const의 차이를 정리하면 다음과 같다.

```
var   : 값 변경 O, 호이스팅 O, 재선언 O
let   : 값 변경 O, 호이스팅 X, 재선언 X
const : 값 변경 X, 호이스팅 X, 재선언 X
```

다시 말하지만, 

호이스팅은 프로그램에 예기치 못한 결과를 야기할 수 있으므로 웬만하면 var 사용은 지양하는것이 좋다.
