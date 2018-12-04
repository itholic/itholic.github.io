---
title: "[go/golang] function (함수)"
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

# 함수

go에서는 함수를 어떻게 쓰면 될까?

간단한 예제를 통해 알아볼까?

숫자를 넣으면 이를 제곱해주는 함수를 만들어보자.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func square(num int) int {
  6     return num * num
  7 }
  8
  9 func main() {
 10     var num = 10
 11     fmt.Println(square(num))
 12 }
```

5번 라인에서 square라는 함수를 선언해, 입력받은 값을 제곱해 돌려주었다.

우선 함수명을 선언하고 소괄호 안에 입력 데이터의 이름과 타입을 적어주었다.

그리고 이어서 리턴 타입을 적어주었다.

리턴 타입은 다음과 같이 소괄호로 묶어 여러개를 명시할 수 있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func square(num int) (string, int) {
  6     return "result", num * num
  7 }
  8
  9 func main() {
 10     var num = 10
 11     fmt.Println(square(num))
 12 }
```

또한 리턴타입에 이름을 붙여서 다음과 같이 리턴도 가능하다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func square(num int) (result string, squared int) {
  6     result = "result"
  7     squared = num * num
  8
  9     return
 10 }
 11
 12 func main() {
 13     var num = 10
 14     fmt.Println(square(num))
 15 }
```

5번 라인을 보면 리턴타입의 이름을 각각 result, squared로 주었다.

그리고 6,7번 라인에서 해당 값들을 할당해주고,

9번 라인에서는 단순히 return 키워드만 입력함으로써 값들을 리턴해주었다.

<br/>

다중 값을 받을 때에는 파이썬과 같이 콤마로 구분해 받을 수 있다.

무슨 말이냐면,

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func square(num int) (result string, squared int) {
  6     result = "result"
  7     squared = num * num
  8
  9     return
 10 }
 11
 12 func main() {
 13     var num = 10
 14     var result, squared = square(num)
 15
 16     fmt.Println(result, squared)
 17 }
```

지금은 인자를 2개 받고있지만,

같은 기능을 하는 함수에 대해 인자를 1개 받고 싶을 때도 있고 3개 받고 싶을 때도 있을 것이다.

python에서는 `"*"` 혹은 `"**"` 키워드를 통해 이를 지원하고있다.

즉, 가변길이 인자를 주고 싶을 때는 어떻게 하면 될까?

go는 `"..."` 키워드를 사용한다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func return_doubled_array(nums ...int) (result []int){
  6
  7     for _, data := range nums {
  8         result = append(result, data * 2)
  9     }
 10
 11     return
 12 }
 13
 14 func main() {
 15     fmt.Println(return_doubled_array(1, 2, 3))
 16     fmt.Println(return_doubled_array(10, 20, 30, 40, 50))
 17 }
```

5번 라인에서 여러 개의 숫자를 받아 각각의 숫자에 2를 곱한 배열을 반환하는 함수를 선언했다.

입력 인자의 타입 앞에 `"..."` 을 붙여주었다.

15번 라인에서 숫자 1, 2, 3을 넘겨주었고, 

16번 라인에서 숫자 10, 20, 30, 40, 50 을 넘겨주었다.

결과를 보자.

```
[2 4 6]
[20 40 60 80 100]
```

정상적으로 작동한다.

'가변길이' 인자라는 말에서 힌트를 얻을 수 있지만,

함수에 여러 값을 넘겨주면 이는 배열이 아닌 '슬라이스' 형태로 들어온다.
