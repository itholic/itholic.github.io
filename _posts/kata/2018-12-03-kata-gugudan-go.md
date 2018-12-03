---
title: "[kata][go] 구구단"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 구구단

출처: <a href="https://www.acmicpc.net/problem/2739" target="_blank">백준 알고리즘 2739번 문제</a>

go 공부를 시작한지 이틀째다.

더 이상의 설명이 필요없는 국민 알고리즘 구구단을 짜보자.

9 이하의 자연수를 받아서 해당 수의 구구단을 출력한다.

<br/>

## 내 풀이

```go
  1 package main
  2
  3 import (
  4     "fmt"
  5 )
  6
  7 var (
  8     num int
  9 )
 10
 11 func main() {
 12     fmt.Scan(&num)
 13
 14     for i := 1; i <= 9; i++ {
 15         fmt.Print(num, " * ", i, " = ", num * i, "\n")
 16     }
 17 }
```

8번째 줄에서 정수 값을 받을 num을 선언했다.

12번째 줄에서 값을 받고,

14번째 줄에서 iteration을 돌며 구구단을 출력했다.


## 다른사람 풀이1

```go
  1 package main
  2
  3 import "fmt"
  4
  5 func main() {
  6     var a int
  7     fmt.Scanf("%d", &a)
  8     for i := 1; i <= 9; i++ {
  9         fmt.Printf("%d * %d = %d\n", a, i, a*i)
 10     }
 11 }
```

변수를 main 함수 안에서 선언하고,

Scanf를 통해 포맷을 지정해서 숫자를 입력받았다.

출력을 할 때에도 Printf를 통해 포맷을 지정해 출력했다.


## 다른사람 풀이2

```go
  1 package main
  2
  3 import (
  4         "bufio"
  5         "fmt"
  6         "os"
  7 )
  8
  9 func main() {
 10         in := 0
 11         fmt.Scan(&in)
 12
 13         b := bufio.NewWriter(os.Stdout)
 14         for i := 1; i <= 9; i++ {
 15                 fmt.Fprintf(b, "%d * %d = %d\n", in, i, in*i)
 16         }
 17         b.Flush()
 18 }
```

bufio, os 모듈을 활용했다.

13번째 줄에서 bufio 모듈의 NewWriter를 통해 쓰기 인스턴스를 생성했다.

이 때, 표준 출력을 인자로 줌으로써 결과 값을 표준 출력으로 보여주게 설정하였다.

저 인자 부분에 file을 넣어주면 결과 값을 파일로 쓸 수 있다고 한다.

15번쨰 줄에 보면 Fprint를 사용하고있는데, 사실 이는 파일 입출력 용도라고 한다.

이 사람은 NewWriter에 파일명대신 표준 출력값을 줌으로써, 파일대신 화면으로 출력하게했다.


## 분석

어느정도 기본 문법에는 익숙해져 가고 있지만,

print 명령어 하나로 퉁치던(?) 파이썬에 비해 print 종류만해도 여러가지라서 아직 많은 혼동을 겪고있다.

일단 가벼운 문제들 위주로 go 기본 문법들에 더 익숙해지는것에 초점을 맞추어야겠다.

번외로, 파이썬으로 같은 프로그램을 짜보았다.

```python
import sys

num = int(sys.stdin.readline())

for i in range(9):
    print(f"{num} * {i+1} = {num * i+1}")
```

내가 아직 go에 익숙하지 못해 효율적인 코드를 짜지 못하는 것도 있지만, 역시 파이썬을 아끼지 않을 수 없다.
