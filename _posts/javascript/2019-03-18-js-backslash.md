---
title: "[javascript] 역슬래시(\) 특수문자"
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


# 역슬래시 특수문자

javascript에서 사용하는 역슬래시 특수문자는 다음과 같은 종류가 있다.

(실제로 '역슬래시 특수문자'가 공식적인 표현은 아니고,

그냥 역슬래시를 포함한 특수문자를 내 편의상 부르는 것이다.)

<br/>

#### 1. `\n`: 개행

사용 예

```javascript
console.log("FirstLine\nSecondLine")
```

실행 결과

```
Firstline
SecondLine
```


#### 2. `\t`: 탭

사용 예

```javascript
console.log("Name\tAge")
console.log("Lee\t30")
```

실행 결과

```
Name    Age
Lee     30
```


#### 3. `\'`, `\"`: 작은 따옴표, 큰 따옴표

사용 예

```javascript
console.log('I didn\'t say, \"Hello, World!\"')
```

실행 결과

```
I didn't say, "Hello, World!"
```

#### 4. `\\`: 역슬래시

사용 예

```javascript
console.log('This is Backslash: \\')
```

실행 결과

```
This is Backslash: \
```

