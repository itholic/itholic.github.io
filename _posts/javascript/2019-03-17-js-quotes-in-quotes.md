---
title: "[javascript] 문자열 안에 따옴표 쓰기"
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


# 문자열 안에 따옴표 쓰기

다음과 같이 문자열 안에 따옴표가 들어가는 경우가 있다.

```javascript
console.log("I said, 'Hello, World!'")
```

문자열 안에 작은따옴표가 들어가있다.

실행하면 다음과 같이 문자열이 정상 출력된다.

```
I said, 'Hello, World!'
```

<br/>

하지만 작은 따옴표대신 큰따옴표가 들어가면 어떻게 될까?

```javascript
console.log("I said, "Hello, World!"")
```

실행해보자.

```
(function (exports, require, module, __filename, __dirname) { console.log("I said, "Hello, World!"")
                                                                          ^^^^^^^^^^

SyntaxError: missing ) after argument list
    at new Script (vm.js:85:7)
    at createScript (vm.js:266:10)
    at Object.runInThisContext (vm.js:314:10)
    at Module._compile (internal/modules/cjs/loader.js:698:28)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:749:10)
    at Module.load (internal/modules/cjs/loader.js:630:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:570:12)
    at Function.Module._load (internal/modules/cjs/loader.js:562:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:801:12)
    at internal/main/run_main_module.js:21:11
```

아주 난리가 난다.

이는 큰따옴표를 문자열 그 자체가 아닌, 문자열을 종료하거나 시작할때 사용하는 문법으로 인식하는 것이다.

문자열 안에 따옴표를 사용하기 위해서는 다음과 같이 역슬래시(\)를 이용해 escape를 해주어야한다.

```javascript
console.log("I said, \"Hello, World!\"")
```

실행하면 문자열이 정상적으로 출력되는 것을 확인할 수 있다.

```
I said, "Hello, World!"
```
