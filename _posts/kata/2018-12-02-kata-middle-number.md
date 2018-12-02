---
title: "[kata][go] 두 번째로 큰 정수 구하기"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 두 번째로 큰 정수 구하기

python의 GIL로 인한 멀티 코어 동시성 프로그래밍의 약점을 보완해보고자, 

go를 한 번 공부해볼까해서 go 튜토리얼겸 간단한 문제를 풀어보았다.

하지만 생각보다 간단하지 않았다(...)

<br/>

출처: <a href="https://www.acmicpc.net/problem/10817" target="_blank">백준 알고리즘 10817번 문제</a>

공백을 기준으로 입력된 세 개의 정수 중, 두 번째로 큰 값을 출력하라.

```
입력
    20 30 10

출력
    20
```    

## 내 풀이

```go
  1 package main
  2
  3 import (
  4     "fmt"
  5     "sort"
  6 )
  7
  8 func main() {
  9     var num_list []int
 10     num_list = make([]int, 3)
 11
 12     fmt.Scanln(&num_list[0], &num_list[1], &num_list[2])
 13
 14     sort.Ints(num_list)
 15
 16     fmt.Print(num_list[1])
 17 }
```

3~6 라인에서 fmt모듈과 sort 모듈을 import하였다.

fmt모듈은 입출력을 위해, sort 모듈은 배열의 정렬을 위함이다.

9번 라인에서 숫자를 받을 배열을 선언하고,

10번 라인에서 슬라이스를 만들었다.

슬라이스는 배열과 거의 같지만, 요소 수를 지정해주어야 한다.

12번 라인에서 슬라이스 각 요소에 공백으로 구분된 정수를 하나씩 할당했다.

14번 라인에서 할당한 정수를 오름차순으로 정렬하고,

16번 라인에서 두 번째 요소(두 번째로 큰 값)를 출력했다.


## 다른사람 풀이1

```go
  1 package main
  2
  3 import (
  4     "fmt"
  5     "sort"
  6 )
  7
  8 var (
  9     a, b, c int
 10 )
 11
 12 func main() {
 13     fmt.Scan(&a, &b, &c)
 14     s := []int{a, b, c}
 15     sort.Ints(s)
 16     fmt.Print(s[1])
 17 }
```

8번 라인을 보면 변수를 선언하는 방식이 특이하다.

main함수 바깥쪽에서 변수를 먼저 선언해줬다.

13번 라인에서 값을 받은 후,

14번 라인에서 슬라이스를 생성했다.

그 이후에는 나와 같이 정렬 후, 2번째 인자를 출력했다.

## 다른사람 풀이2

```go
  1 package main
  2
  3 import "fmt"
  4 import "sort"
  5
  6 func main() {
  7     var a []int = make([]int, 3)
  8     for i := 0; i < 3; i++ {
  9         fmt.Scan(&a[i])
 10     }
 11
 12     sort.Ints(a)
 13
 14     fmt.Println(a[1])
 15 }
```

다 비슷한 방식이긴 하지만, 이번에는 for문을 활용했다.

go를 처음 공부하는 것이기 때문에 for문 사용법을 참고하자는 의미에서 가져왔다.


## 분석

첫 go 코딩인 만큼, 부담가지지 않고 문법에 익숙해지자는 취지로 시작했다.

사실 python처럼 문자열을 받아서 split 한 다음, sort하면 끝날 줄 알았다.

파이썬에 익숙한 사람이면 금방 배울거라는 말에 정말 가볍게 훑어봤는데,

생각보다 까탈스러운 부분이 좀 있어서 간단한 코딩을 하는데에도 애를 좀 먹었다.

<br/>

일단 가장 충격받은것은 import한 모듈을 사용하지 않으면 Error가 발생한다.

Warning이 아니다. Error다.

하지만 처음 접하는 사용자 입장에서 다소 불편하긴해도, 나쁘지 않다고 생각한다.

컨벤션을 강제하는 느낌이랄까?

어느 면에선 꽤나 매력적인(?) 부분이다.

<br/>

변수를 선언하는 방식도 상당히 낯설어서 차분히 익혀 나가야겠다.

그리고 배열과 슬라이스를 굳이 나누어놓은 이유도 잘 와닿지 않아, 이 부분도 다시 공부해봐야겠다.

<br/>

java를 하다가 python으로 넘어갈때와 확실히 다른 느낌이다.

파이썬의 약점인 다중 코어 동시성 프로그래밍을 보완할 수 있다는 말에 혹해서 가벼운 마음으로 시작했는데, 

생각보다 각잡고 빡시게 공부해야 뭐라도 건질게 있을 것 같다는 생각이 든다.
