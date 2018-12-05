---
title: "[go/golang] 배열, 슬라이스, 맵 (array, slice, map)"
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

# 배열, 슬라이스, 맵

go에서는 기본 타입 이외에도 배열, 슬라이스, 맵이라는 세 가지 타입을 지원한다.

일단 배열은 고정길이 배열을 의미한다.

그리고 슬라이스가 가변길이 배열이다.

python에서 사용하던 list를 생각하면 된다.

맵은 key-value형태의 자료형으로 python에서 사용하던 dict를 생각하면 된다.

사용법을 알아보자.

## 배열

배열은 고정길이 배열이다.

다음과 같이 쓰면 된다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     var arr_int [5]int
  7     fmt.Println(arr_int)
  7     fmt.Println(len(arr_int))
  8 }
```

arr_int라는 이름의 길이 5짜리 배열을 선언하고, 출력했다.

배열의 길이를 구하는 메소드인 len()을 사용해 배열의 길이도 출력했다.

또한 일반 자료형과는 달리 `var 변수명` 뒤에 자료형을 생략할 수 없다.

`var arr_int [5]` 와 같이 쓸 수 없다는 뜻이다.

출력 결과는 다음과 같다.

```
[0 0 0 0 0]
5
```

값을 지정해주지 않으면 0으로 초기화된다는것을 알 수 있다.

배열의 각 요소는 일반적인 방식처럼 대괄호를 통해 접근 가능하다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     var arr_int [5]int
  7     for i := 0; i < len(arr_int); i++ {
  8         arr_int[i] = i
  9     }
 10     fmt.Println(arr_int[0])
 11     fmt.Println(arr_int[1])
 12     fmt.Println(arr_int[2])
 13     fmt.Println(arr_int[3])
 14     fmt.Println(arr_int[4])
 15 }
```

7번 라인에서 배열의 길이만큼 iteration을 돌며 배열의 각 요소에 값을 할당했다.

그리고 10번 라인부터 차례대로 배열의 요소를 출력했다.

결과는 다음과 같다.

```
0
1
2
3
4
```

출력하는 부분은 다음과 같이 for문과 range 키워드를 통해 간소화 할 수 있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     var arr_int [5]int
  7     for i := 0; i < len(arr_int); i++ {
  8         arr_int[i] = i
  9     }
 10
 11     for _, data := range arr_int {
 12         fmt.Println(data)
 13     }
 14 }
```

마치 파이썬에서 `for i, data in enumerate(arr_int)` 를 쓰는 것과 비슷한 형태로,

배열의 인덱스 값과 데이터 값을 가지고 iteration을 돌릴 수 있다.

현재 인덱스번호는 사용하고있지 않으므로 언더바 `_`를 통해 컴파일러에게 명시적으로 알려주었다.

현재 상태에서 `_` 대신  `i`나 `idx`같은 변수를 쓰면 에러가 난다 (선언만하고 사용되지 않았으므로)

<br/>

다시 배열 이야기로 돌아와서,

배열은 다음과 같이 선언과 동시에 초기화해줄수있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := [5]int{0, 1, 2, 3, 4}
  7
  8     for data := range arr_int {
  9         fmt.Println(data)
 10     }
 11 }
```

6번 라인을 보면, 길이 5짜리 int 배열을 선언과 동시에 초기화했다.

## 슬라이스

슬라이스는 가변길이 배열이라고 했었다.

다음가 같이 make 메소드를 사용해 생성할 수 있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := make([]int, 5)
  7
  8     fmt.Println(arr_int)
  9 }
```

얼핏보면 배열의 예제와 똑같지만, 

6번 라인에서 `var arr_int [5]int` 대신 make 함수를 통해 슬라이스를 생성하고있다.

물론 make함수를 사용하지 않아도 된다. 

`arr_int := []int{1, 2, 3, 4, 5}` 와 같은 형태로 길이를 명시하지 않고 선언하면 배열대신 슬라이스가 생성된다.

하지만 일단은 해당 예제를 보고 아래에서 추가적으로 설명하도록 하겠다.

실행시켜보면 다음과 같은 결과가 나온다.

```
[0 0 0 0 0]
```

근데 이러면 길이 5짜리 배열을 선언한것과 다를게 없어보인다.

대체 배열과 슬라이스는 뭐가 다른걸까?

왜 슬라이스는 '가변길이' 배열이라고 부르는 것일까?

다음 코드를 보자.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := make([]int, 5, 10)
  7     x := arr_int[0:10]
  8
  9     fmt.Println(arr_int)
 10     fmt.Println(x)
 11 }
```

6번 라인을 보면 세 번째 인자에 10이 추가됐다.

이는 슬라이스의 최대 길이는 10으로 하겠다는 의미이고, 

일단은 길이 5의 슬라이스를 만들겠다는 의미이다.

<br/>

7번 라인을 보면 기존에 생성한 슬라이스 arr_int를 통해 새로운 슬라이스 x를 생성하고있다.

실행 결과를 보면 arr_int는 `[0 0 0 0 0]`, x는 `[0 0 0 0 0 0 0 0 0 0]` 이 출력된다.

만약 10보다 큰 값을 주어 `y := arr_int[0:11]`과 같이 생성하면 다음과 같은 에러가 발생한다.

```
panic: runtime error: slice bounds out of range
```

slice 범위를 벗어났다는 에러이다.

즉, slice는 고정길이 배열과 달리 초기화시 최대 길이를 지정할 수 있고,

해당 slice를 통해 최대 길이를 넘지 않는 범위에서 가변길이 배열(=슬라이스)을 얼마든 생성해낼 수 있다.

물론, 아래에서 설명할 append같은 메소드를 사용하면 슬라이스의 길이를 확장시킬 수 있다.

<br/>

나도 완벽하게 이해한것은 아니지만, 말이 어렵다면 일단 python의 list랑 같다고 생각해도 무리가 없는 것 같다.

그냥 list라고 생각하고 다시 보면 그대로 이해가 된다.

아마 배열의 일부를 '잘라서' 원하는 길이만큼 사용한다는 의미로 slice라는 이름이 붙은 것 같다.

실제로 파이썬의 iterable한객체를 slice해서 사용하는 것과 동일하게 `":"` 키워드를 사용하고있다.

<br/>

slice는 배열과 마찬가지로 다음과 같이 선언과 동시에 초기화 할 수 있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := []int{1, 2, 3, 4, 5}
  7
  8     fmt.Println(arr_int)
  9 }
```

배열에서는 `arr_int := [5]int{1, 2, 3, 4, 5}`와 같은 형태로 선언했었다.

int의 길이를 명시하는 않은 부분만 다르다.

그리고 slice로 선언하면 다음과 같은 함수를 사용할 수 있다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := []int{1, 2, 3, 4, 5}
  7
  8     x := append(arr_int, 6, 7, 8, 9, 10)
  9
 10     fmt.Println(arr_int)
 11     fmt.Println(x)
 12 }
```

append함수를 이용해 슬라이스 arr_int를 확장시킨 슬라이스 x를 생성했다.

즉, 길이 5짜리 슬라이스를 선언했지만 append메소드를 통해 길이 10으로 확장한 것이다.

실행 결과는 다음과 같다.

```
[1 2 3 4 5]
[1 2 3 4 5 6 7 8 9 10]
```

python에서 list뒤에 값을 append하는것을 생각해보면 똑같은 논리로 작동한다는 것을 알 수 있다.

슬라이스는 copy라는 메소드를 제공해 슬라이스의 복사를 지원한다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := []int{1, 2, 3, 4, 5}
  7
  8     x := make([]int, 10)
  9     y := make([]int, 3)
 10
 11     fmt.Println("x before copy: ", x)
 12     fmt.Println("y before copy: ", y)
 13
 14     copy(x, arr_int)
 15     copy(y, arr_int)
 16
 17     fmt.Println()
 18     fmt.Println("x after copy: ", x)
 19     fmt.Println("y after copy: ", y)
 20 }
```

8, 9 번 라인에서 길이 10짜리 슬라이스 x와 길이 3짜리 슬라이스 y를 선언했다. 

그리고 14, 15번 라인에서 arr_int를 각 슬라이스 x, y에 복사했다.

결과를 보자.

```
x before copy:  [0 0 0 0 0 0 0 0 0 0]
y before copy:  [0 0 0]

x after copy:  [1 2 3 4 5 0 0 0 0 0]
y after copy:  [1 2 3]
```

슬라이스 arr_int의 값이 그대로 복사된 것을 확인할 수 있다.

길이 3짜리 슬라이스에는 세 번째 데이터까지만 복사되었다.

만약 append, copy와 같은 메소드를 슬라이스가 아닌 배열에 적용하면 어떻게 될까?

배열에 append메소드를 적용해보자.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     arr_int := [5]int{1, 2, 3, 4, 5}
  7
  8     x := append(arr_int, 6 ,7, 8, 9, 10)
  9
 10     fmt.Println(arr_int)
 11     fmt.Println(x)
 12 }
```

길이 5짜리 배열에 append메소드를 사용해 6, 7, 8, 9, 10 을 추가하고자 한다.

위 코드를 실행시키면 다음과 같은 에러가 발생한다.

```
# command-line-arguments
./main.go:8:16: first argument to append must be slice; have [5]int
```

append 메소드는 slice에만 적용 가능하다고 한다.

위 코드 6번 라인의 `[5]` 부분만 `[]`로 변경하면 정상 작동한다.

<br/>

쉽게 생각해서, 

리스트를 선언할때 길이를 명시해주면 '배열'이 생성되며 명시한 숫자만큼의 길이만 사용할 수 있다.

하지만 길이를 명시하지 않으면 '슬라이스'가 생성되며 길이를 유연하게 조정하며 사용할 수 있다.

## 맵

마지막으로 맵을 알아보자.

맵은 key - value 쌍으로 된 데이터 타입으로, 파이썬의 dict를 생각하면 된다.

맵은 다음과 같이 사용한다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     map_int_str := make(map[int]string)
  7     map_int_str[1] = "월"
  8     map_int_str[2] = "화"
  9     map_int_str[3] = "수"
 10     map_int_str[4] = "목"
 11     map_int_str[5] = "금"
 12     map_int_str[6] = "토"
 13     map_int_str[7] = "일"
 14     fmt.Println(map_int_str)
 15 }
```

make 메소드를 통해 map을 선언하고, 값을 할당했다.

map키워드 다음에 key로 사용될 변수의 타입을 대괄호 안에 넣어준다.

마지막으로 value로 사용될 변수의 타입을 이어서 적어주면 된다.

6번 라인을 해석하자면, 

"key의 자료형이 int이고, value의 자료형이 string인 map을 만들어라" 정도가 되겠다.

다음과 같이 선언과 동시에 초기화도 가능하다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     map_int_str := map[int]string {
  7         1: "월",
  8         2: "화",
  9         3: "수",
 10         4: "목",
 11         5: "금",
 12         6: "토",
 13         7: "일",
 14     }
 15     fmt.Println(map_int_str)
 26 }
```

선언과 동시에 `":"` 키워드를 이용해서 key: value 쌍을 초기화했다.

참고로, 13번째 줄처럼 마지막 요소에도 콤마를 찍어주지 않으면 에러가 발생한다.

map에 있는 요소는 다음과 같이 사용하면 된다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     map_int_str := map[int]string {
  7         1: "월",
  8         2: "화",
  9         3: "수",
 10         4: "목",
 11         5: "금",
 12         6: "토",
 13         7: "일",
 14     }
 15     fmt.Println(map_int_str[1])
 16     fmt.Println(map_int_str[2])
 17     fmt.Println(map_int_str[3])
 18     fmt.Println(map_int_str[4])
 19     fmt.Println(map_int_str[5])
 20     fmt.Println(map_int_str[6])
 21     fmt.Println(map_int_str[7])
 22 }
```

결과는 다음과 같다.

```
월
화
수
목
금
토
일
```

근데 만약 다음과 같이 없는 요소를 꺼내오려고 하면 어떻게 될까?

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     map_int_str := map[int]string {
  7         1: "월",
  8         2: "화",
  9         3: "수",
 10         4: "목",
 11         5: "금",
 12         6: "토",
 13         7: "일",
 14     }
 15     fmt.Println(map_int_str[8])
 16 }
```

go가 엄청 깐깐한(?)언어라서 에러가 날줄 알았는데,

또 이런 부분에서는 그냥 공백("")을 리턴한다.

숫자의 경우에는 0을 리턴한다.

그래서 `map_int_str[8] == ""` 과 같이 잡아서 처리할수도 있겠지만,

사실 맵의 탐색 결과는 두 가지 값을 리턴한다.

무슨 말인지 확인해보자.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     map_int_str := map[int]string {
  7         1: "월",
  8         2: "화",
  9         3: "수",
 10         4: "목",
 11         5: "금",
 12         6: "토",
 13         7: "일",
 14     }
 15     value, ok := map_int_str[1]
 16     fmt.Println(value, ok)
 17     value, ok = map_int_str[5]
 18     fmt.Println(value, ok)
 19     value, ok = map_int_str[8]
 20     fmt.Println(value, ok)
 21 }
```

15번, 17번 라인에서는 map_int_str에 존재하는 key 값인 1과 5를 기준으로 탐색했다.

하지만 19번 라인에서는 map_int_str에 존재하지 않는 key값인 8을 기준으로 탐색했다.

그리고 모든 경우에 대해 value, ok  라는 두 개의 값을 받아서 출력했다.

결과를 보자.

```
월 true
금 true
 false
```

key가 1일떄 value는 '월' ok 는 true가 반환됐다.

key가 5일떄 value는 '금' ok 는 true가 반환됐다.

key가 8일떄 value는 ''(공백) ok 는 false가 반환됐다.

즉, 존재하지 않는 key에대한 값을 요구하면 두 번째 인자로 false를 반환한다.

그래서 일반적으로 go에서는 다음과 같은 형태로 예외를 걸러낸다고 한다.

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     map_int_str := map[int]string {
  7         1: "월",
  8         2: "화",
  9         3: "수",
 10         4: "목",
 11         5: "금",
 12         6: "토",
 13         7: "일",
 14     }
 15
 16     for key := 0; key < 10; key++ {
 17         if value, ok := map_int_str[key]; ok {
 18             fmt.Println(value)
 19         } else {
 20             fmt.Println("key", key, "is not exist")
 21         }
 22     }
 23 }
```

16번 라인에서 iteration하며 map_int_str의 key로 0부터 9까지 대입했다.

map_int_str[key]의 결과로 value와 ok값을 받아서,

ok가 true일 경우(해당 key에대한 value가 존재할 경우) key에 해당하는 value를 출력한다.

그렇지 않은경우, "key is not exist" 와 같은 문자열을 출력한다.

결과는 다음과 같다.

```go
key 0 is not exist
월
화
수
목
금
토
일
key 8 is not exist
key 9 is not exist
```

이미 자주 사용하던 자료형들인데도 조금씩 사용 방법이 다르다.

파이썬에 비교하자면 사용적인 측면에서는 다소 불편한 점도 있지만,

타입이 명시적이고, 각 요소를 세밀하게 조작 가능한만큼 성능적인 측면에서 확실히 유리할 것 같다는 생각이 든다.

