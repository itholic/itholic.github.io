---
title: "[javascript] 여러 줄 문자열"
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


# 여러 줄 문자열

javascript에서 여러 줄에 걸쳐 문자열을 쓰는 방법은 몇 가지가 있다.

먼저, 역슬래시`(\)`를 이용한 방법이다.

```javascript
console.log("First Line\
Second Line\
Third Line")
```

실행 결과

```
First LineSecond LineThird Line
```

여러 줄에 걸쳐 코드를 작성할 수는 있지만,

보시다시피 출력을 할 때 개행이 되지는 않는다.

개행을 하려면 다음과 같이 개행문자를 추가해주어야한다.

```javascript
console.log("First Line\n\
Second Line\n\
Third Line")
```

실행 결과

```
First Line
Second Line
Third Line
```

이번엔 코드의 가독성을 위해 들여쓰기를 좀 해보자.

```javascript
console.log("First Line\n\
            Second Line\n\
            Third Line")
```

실행 결과

```
First Line
            Second Line
            Third Line
```

실행 결과에도 들여쓰기가 그대로 적용되어 가독성이 영 좋지 않아보인다.

<br/>

그렇다면 좀 더 직관적인 방법은 없을까?

이번엔 백틱`(\`)`을 사용해보자.


```javascript
console.log(`First Line
Second Line
Third Line`)
```

실행 결과

```
First Line
Second Line
Third Line
```

코드가 한결 깔끔해졌다.

하지만 이번에도 코드를 들여쓰기하면 어떻게될까?

```javascript
console.log(`First Line
            Second Line
            Third Line`)
```

실행 결과

```
First Line
            Second Line
            Third Line
```

역슬래쉬 방법과 마찬가지로,

실행 결과에도 들여쓰기가 그대로 적용되어 원하는 결과가 나오지 않았다.

<br/>

역슬래쉬를 이용한 방식은 개행문자를 일일이 추가해주어야한다는 단점이 있다.

게다가 코드를 들여쓰기하게 되면 출력 결과에도 들여쓰기 공백이 그대로 출력된다.

백틱을 이용한 방식은 개행문자를 일일이 추가하지 않아도 되지만,

마찬가지로 코드의 들여쓰기가 실제 출력 결과에 그대로 반영된다.

<br/>

그렇다면 코드의 가독성도 어느정도 유지하면서, 상식적인 출력 결과를 내려면 어떻게 하는게 좋을까?

```javascript
console.log("First Line\n" +
            "Second Line\n" +
            "Third Line")
```

실행 결과

```
First Line
Second Line
Third Line
```

개행문자를 직접 입력해주어야 한다는 단점이 있지만,

들여쓰기를 통한 코드의 가독성을 확보할 수 있고,

또한 실행 결과도 코드를통해 직관적으로 예측가능한 형태로 출력되고있다.

하지만 어떤 방법이 최고라고는 할 수 없다.

본인의 취향에 맞는 방식을 골라 여러 줄 문자열을 표현해주면 된다.
