---
title: "[go/golang] variable (변수)"
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

# 변수

첫 go 포스팅이니만큼 조금의 사족을 달아보자.

최근 며칠간 kata와 구글링을 통해 go를 주먹구구식으로 공부했었는데,

이게 생각보다 각잡고 공부해야 뭔가 얻을게 있을 것 같다는 생각이 들었다.

얼마나 속도가 날지는 모르겠지만 관련 지식이 쌓일때마다 천천히 정리해보고자 한다.

카테고리가 너무 많아져서 정신없어지는 것 같긴 하지만 필요한건 해야지 ㅠ

<br/>

이제 본론으로 들어가자.

변수는 사실 여타 언어에서 지원하는 그것들과 다를바 없다.

다만 표현 방식이 조금 특이하다.

코드를 보자.

```go
  1 package main
  2
  3 func main() {
  4     var x string = "a"
  5     var y = "b"
  6     z := "c"
  7 }
```

4번라인을 보면 var 키워드 뒤에 변수명을 적어주고, 이어서 타입을 적어주었다.

참고로 이 경우에는 `var x string` 처럼 변수를 선언만하고 초기화는 나중에 할 수 있다.

5번라인에서는 변수명을 생략했다.

이 경우는 할당되는 값을 토대로 타입을 추론하므로, 반드시 선언과 동시에 초기화해야한다.

마지막으로 6번 라인에서는 `:=` 라는 키워드를 사용했는데, 5번라인의 방식과 동일하게 동작한다.

<br/>

다 좋은데, 이대로 코드를 실행시키면 다음과 같은 에러가 발생한다.

```
# command-line-arguments
./main.go:4:9: x declared and not used
./main.go:5:9: y declared and not used
./main.go:6:5: z declared and not used
```

변수를 선언만하고 사용하지 않았다는 에러이다.

변수를 선언을 했으면 무조건 사용해야한다.

마찬가지로 모듈도 import를 했으면 무조건 사용해야한다.

안그러면 warning이 아니라 아예 error다.

<br/>

python의 경우 flake8이나 pylint등을 통해 정적분석을 할때나 warning으로 알려주는 부분,

즉, 일종의 컨벤션과 비슷한 부분인데, go에서는 이것이 강제된다.

<br/>

어쨌든 다음과 같이 fmt라는 입출력 포매팅 관련 모듈을 사용해서 출력해주면 제대로 실행된다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     var x string = "a"
  7     var y = "b"
  8     z := "c"
  9     fmt.Println(x, y, z)
 10 }
```

참고로 fmt는 표준입출력, 파일입출력등 다양한 입출력을 지원하는 모듈인데,

입출력파일 포맷을 정해주는 'formatter' 의 줄임말 정도로 생각하면 될 것 같다.

<br/>

변수는 다음과 같이 함수 바깥쪽에 선언할수도 있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 var x string = "a"
  6 var y = "b"
  7
  8 func main() {
  9     z := "c"
 10     fmt.Println(x, y, z)
 11 }
```

이는 다른 함수에서도 해당 변수들에 접근 가능하다는 뜻이다.

참고로 var 키워드로 시작되는 방식만 바깥에 선언 가능하다.

`:=` 키워드는 함수 안쪽에서만 선언 가능하다.

<br/>

비슷한 맥락에서 `var x string` 같은 방식의 경우, 

바깥쪽에 따로 변수를 선언할수는 있지만, 초기화는 함수 안쪽에서만 가능하다.

예를들어 다음의 코드는 에러가 발생한다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 var x string
  6 x = "a"
  7 var y = "b"
  8
  9 func main() {
 10     z := "c"
 11     fmt.Println(x, y, z)
 12 }
```

```
# command-line-arguments
./main.go:6:1: syntax error: non-declaration statement outside function body
```

또한 다음과 같은 선언도 가능하다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 var (
  6     x string = "a"
  7     y = "b"
  8     z = "c"
  9 )
 10
 11 func main() {
 12     fmt.Println(x, y, z)
 13 }
```

사용할 변수를 모두 var 키워드로 묶어서 바깥쪽에서 선언했다.

마지막으로 상수를 선언할 때에는 const 키워드로 선언하면 된다.

상수는 반드시 선언과 동시에 초기화 해주어야하며, 값을 변경할 수 없다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     // const X
  7     const X = 10
  8     // X = 20
  9     fmt.Println(X)
 10 }
```

6번라인은 상수 선언과 동시에 초기화를 하지 않아서 에러,

8번라인은 이미 선언된 상수에 값을 할당하려고 해서 에러다.

<br/>

주먹구구식으로 예제코드를 보며 kata를 할 때에는 마냥 복잡하기만 했는데,

개념을 차근차근 정리하다보니 생각보다 간단하고 매력있는 언어라는 생각이 든다.
