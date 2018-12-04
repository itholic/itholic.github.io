---
title: "[go/golang] for, if, switch (흐름제어)"
layout: post
tag:
- go
- golang
category: go
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 흐름제어

go에서는 for문과 if문을 어떻게 쓸까?

바로 코드를 보면 될 것 같다.

## for

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     for i := 1; i <= 10; i++ {
  7         fmt.Println(i)
  8     }
  9 }
```

한동안 파이썬만 하다가 C나 JAVA스러운(?) for문을 보니 반갑다. (편하고 불편하고를 떠나서ㅎㅎ)

사실 그냥 일반적인 언어에서의 사용방법과 크게 다르지 않아 딱히 설명할부분이 없다.

for문에서 반복시킬 값을 초기화 하고, 반복 조건을 주고, 반복 완료시 취할 동작을 명시했다.

for문 뒤에 소괄호가 없다는 점에서 파이썬과 비슷하면서도 중괄호로 동작부분을 감싼다는 점에서 C, JAVA와 비슷하다.

## if

위 코드에 if문을 추가해 짝수일떄 "i, 짝수" 홀수일때 "i, 홀수" 라고 출력해보자.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     for i := 1; i <= 10; i++ {
  7         if i % 2 == 0 {
  8             fmt.Println(i, ", 짝수")
  9         } else {
 10             fmt.Println(i, ", 홀수")
 11         }
 12     }
 13 }
```

마찬가지로 if문의 사용법도 여타 언어에서의 그것과 다를바 없다.

아, 참고로 `else if` 문도 지원하니 참고하자.

## switch ~ case

마지막으로 이건 정말 반가운 기능인데, switch ~ case를 지원한다.

물론 파이썬에서도 switch ~ case와 비슷하게 사용할 수 있긴 하지만 (<a href="https://itholic.github.io/python-switch-case/" target="_blank">파이썬에서 switch~case 사용하기</a>),

자체적인 문법을 지원하는 경우는 확실히 편리하다.

다음과 같이 쓰면 된다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     var i int
  7     fmt.Scan(&i)
  8     switch i {
  9         case 1: fmt.Println("월")
 10         case 2: fmt.Println("화")
 11         case 3: fmt.Println("수")
 12         case 4: fmt.Println("목")
 13         case 5: fmt.Println("금")
 14         case 6: fmt.Println("토")
 15         case 7: fmt.Println("일")
 16         default: fmt.Println("7 이하의 자연수만 가능")
 17     }
 18 }
```

6번째 줄에서 int형 변수를 담을 i를 선언하고,

7번째 줄에서 `fmt.Scan` 메소드를 통해 입력을 받는다.

<br/>

i에 1~7사이의 숫자가 입력되면 월~일 까지의 날짜를 매핑하여 출력해준다.

숫자가 조건 안에 없을 때에는 default 값을 주어 예외를 처리한다.
