---
title: "[kata][go] 곱해진 결과에 포함된 숫자의 갯수"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 곱해진 결과에 포함된 숫자의 갯수

출처: <a href="https://www.acmicpc.net/problem/2577" target="_blank">백준 알고리즘 2577번 문제</a>

숫자 세 개를 입력받아 곱하고,

곱해진 결과에 0부터 9까지 정수가 각각 몇 번씩 들어갔는지 출력.

예를들어 4 5 6 을 입력받았다면,

세 수를 곱한 120에 0부터 9까지 정수가 몇 번 들어갔는지 출력한다.

0은 한 번, 1도 한 번, 2도 한 번, 3~9까지 0번 들어갔다.

이 경우 결과는 `1 1 1 0 0 0 0 0 0 0` 으로 나오면 된다.

```
입력
    150 266 427

출력
    3
    1
    0
    2
    0
    0
    0
    2
    0
    0
```

<br/>

## 내 풀이

```go
  1 package main
  2
  3 import (
  4     "fmt"
  5     "strings"
  6     "strconv"
  7 )
  8
  9 var (
 10     a int
 11     b int
 12     c int
 13 )
 14
 15 func main() {
 16     fmt.Scan(&a, &b, &c)
 17     abc := strconv.Itoa(a * b * c)
 18     abc_splitted := strings.Split(abc, "")
 19
 20     for i := 0; i < 10; i++ {
 21         num_cnt := 0
 22         for j := 0; j < len(abc_splitted); j++ {
 23             if value, _ := strconv.Atoi(abc_splitted[j]); value == i {
 24                 num_cnt++
 25             }
 26         }
 27         fmt.Println(num_cnt)
 28     }
 29 }
```

우선 입출력을 위한 fmt모듈, 문자열을 슬라이스로 담기위한 strings 모듈, 문자열 형변환을위한 strconv 모듈을 import 했다.

변수는 정수형 변수 a, b, c 세 개를 선언했다.

16번째 줄에서 값을 받고, 17번째 줄에서 세 값을 곱한 결과를 abc라는 string으로 변형했다.

18번째 줄에서 변형한 문자열을 split해서 abc_splitted라는 슬라이스로 만들었다.

20번째 줄에서 0부터 9까지 iteration을 돌며 비교 작업을 시작하고,

22번째 줄에서 잘라진 문자열의 갯수만큼 iteration을 돌며 각 자리 숫자와 바깥쪽 for문에서 넘어온 정수가 일치하는지 비교한다.

23번째 줄을 보면 strconv.Atoi는 변형한 값과 에러 여부를 반환하므로, 

value와 _ 를 받아주고 value가 비교대상인 정수인 경우 카운트를 1개씩 추가했다.

27번째 줄에서 0~9까지의 각 iteration마다 결과를 출력했다.

## 다른사람 풀이

```go
  1 package main
  2
  3 import (
  4     "fmt"
  5 )
  6
  7 func main() {
  8     var a, b, c int
  9     fmt.Scanf("%d", &a)
 10     fmt.Scanf("%d", &b)
 11     fmt.Scanf("%d", &c)
 12
 13     var appearance [10]int
 14     multiple := a * b * c
 15
 16     for multiple > 0 {
 17         appearance[multiple%10]++
 18         multiple /= 10
 19     }
 20
 21     for _, v := range appearance {
 22         fmt.Println(v)
 23     }
 24 }
```

13번째 줄에서 appearance라는 이름의 길이 10짜리 배열을 선언했다.(초기값 전부 0)

14번째 줄에서 a, b, c를 받아 곱한 수를 multiple 변수에 담았다.

16번째 줄에서 multiple에 대해 iteration을 돌렸다.

17번째 줄에서 multiple을 10으로 나눈 값의 나머지, 즉, 1의자리수를 구하고,

appearance의 해당 index번호를 1개씩 증가시켰다.

예를들어 1의자리수가 3이었다면, appearance[3] 을 한 개 증가시킨 것이다.

그리고 18번째 줄에서 1의자리를 버린 값(multiple을 10으로 나눈 몫)을 다시 multiple 변수에 넣어주었다.

multiple이 0이 될때까지 반복하다보면, 모든 자리수를 체크해서 appearance의 각 인자에 0~9까지 정수가 몇 번 등장했는지 계산할 수 있다.

## 분석

일단 메모리 효율이 내가 작성한 코드가 거의 4배정도 좋게 나왔다.

물론 성능적인 측면은 확인하기 어려워서 내 방식이 무조건 좋다고 할수는 없다.

<br/>

메모리적인 측면에서만 나름 분석을 해보자면,

내 코드는 1개의 슬라이스(세 개의 수를 곱한 값의 문자열 슬라이스)를 사용했고,

다른 사람의 코드는 1개의 배열(0이 10개담긴 배열)을 사용했다.

<br/>

여기까진 큰 차이가 없어보이는데, 

내 코드는 매 iteration마다 각 문자열의 값을 i값과 비교하여 카운트를 증가시키고 그것을 바로 출력한 반면,

다른 사람의 코드는 매 iteration마다 배열의 값을 바꿔주고, 최종적으로 완성된 배열을 다시 iteration돌며 출력했다.

아마 이 부분에서 메모리의 차이가 난 것 같아서, 

효율성의 차이라기보다는 상황에따라 바로 출력하느냐 담아뒀다 출력하느냐에서 발생한 차이인 것 같다.

<br/>

내 코드는 int와 string 자료형을 계속 변환하기때문에, 

코드가 길어지면 내 코드가 성능적으로 이슈가 될 수 있지 않을까 하는 생각이 든다.

무조건 문자열을 잘라 슬라이스를 만드는 방식보다는 다른사람 코드처럼 수학적으로 접근하는 방법도 나쁘지 않은 것 같다.
