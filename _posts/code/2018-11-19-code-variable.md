---
title: "[code] variable (변수)"
layout: post
tag:
- code
category: code
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---


# Variable


각 언어별 간단한 변수 선언 예제

추가 학습시 계속 업데이트 예정

<br/>

**C**

C는 운영체제에따라 자료형의 크기가 달라지므로 유의해야한다.

char는 정수 자료형으로 분류되지만, 문자 하나를 저장할 수 있다.

문자 하나는 암시적으로 1바이트 정수로 변환 가능하기 때문이다.

```c
#include <stdio.h>

#define CONST 10  // 10이라는 상수를 CONST라는 변수에 선언


int main()
{
    // +, - 부호가 있는 정수 자료형
    char num1;  // 1바이트
    short num2;  // 2바이트
    int num3;  // 4바이트 (운영체제의 비트 수에 맞춤, 하지만 4바이트를 초과하지는 않음)
    long num4;  // 8바이트 (운영체제가 64비트일 경우의 크기, 하지만 windows에서는 여전히 4바이트임)

    // - 부호가 없는 정수 자료형, 크기는 상동
    unsigned char num5;
    unsigned short num6;
    unsigned int num7;
    unsigned long num8;

    // 실수 자료형
    float num9;  // 4바이트
    double num10;  // 8바이트
    long double num11;  // 12바이트 (운영체제가 96비트일 경우의 크기, 일반적으로는 8바이트)

    // boolean
    bool flag;  // 1(true), 0(false)

    return 0;
}
```

<br/>

**C#**

C#은 상수 선언시 C, C++과 달리 #define 키워드를 지원하지 않는다.

모든 변수 앞에 const 키워드를 붙여서 상수로 선언 가능하다.

```c#
using System;


namespace HelloWorld
{
    class Hello {         
        static void Main(string[] args)
        {
            // 문자열
            string str;

            // +, - 부호가 있는 정수 자료형
            sbyte num1;  // 1바이트
            short num2;  // 2바이트
            int num3;  // 4바이트
            long num4;  // 8바이트
        
            // - 부호가 없는 정수 자료형, 크기는 상동
            byte num5;
            ushort num6;
            uint num7;
            ulong num8;
        
            // 실수 자료형
            float num9;  // 4바이트
            double num10;  // 8바이트
            decimal num11;  // 16바이트

            // boolean
            bool flag;  // 1(true), 0(false)
        }
    }
}
```

<br/>

**C++**

C++의 변수 표현 방식은 C와 동일하다.

그리고 모든 변수 앞에 const 키워드를 붙여서 상수로 선언 가능하다.

```cpp
#include <iostream>

#define CONST 10  // 10이라는 상수를 CONST라는 변수에 선언


int main()
{
    // 문자열
    string str;

    // +, - 부호가 있는 정수 자료형
    char num1;  // 1바이트
    short num2;  // 2바이트
    int num3;  // 4바이트 (운영체제의 비트 수에 맞춤, 하지만 4바이트를 초과하지는 않음)
    long num4;  // 8바이트 (운영체제가 64비트일 경우의 크기, 하지만 windows에서는 여전히 4바이트임)

    // - 부호가 없는 정수 자료형, 크기는 상동
    unsigned char num5;
    unsigned short num6;
    unsigned int num7;
    unsigned long num8;

    // 실수 자료형
    float num9;  // 4바이트
    double num10;  // 8바이트
    long double num11;  // 12바이트 (운영체제가 96비트일 경우의 크기, 일반적으로는 8바이트)

    // boolean
    bool flag;  // 1(true), 0(false)

    return 0;
}
```

<br/>

**JAVA**

```java
public class HelloWorld{
    public static void main(String args[]) {
        // 문자 자료형
        char foo;  // 2바이트

        // +, - 부호가 있는 정수 자료형
        byte num1;  // 1바이트
        short num3;  // 2바이트
        int num4;  // 4바이트
        long num5;  // 8바이트

        // 실수 자료형
        float num6;  // 4바이트
        double num7;  // 8바이트
    }
}
```


<br/>

**JAVASCRIPT(NODE)**

javascript는 기본적으로 var라는 키워드에 모든 변수를 선언한다.

let, const등의 키워드를 통해 더 상세한 핸들링을 지원한다.

이는 <a href="https://itholic.github.io/js-var-let-const/" target="_blank">따로 포스팅한 내용</a>이 있으니 참고하면 될 것 같다.

```js
var str = "string";
var num1 = 123;
var num2 = 123.456;
var flag = true;
```

<br/>

**PYTHON**

python은  그냥 변수를 선언하고 원하는 값을 담아주면 자동으로 int, long, float 등의 타입이 할당된다.

참고로 세미콜론(;)도 사용하지 않는다.

```python
str1 = "string"
num1 = 123
num2 = 123.456
flag = TRUE
```

<br/>

**R**

```r
str <- "string"
num1 <- 123
num2 <- 123.456
flag <- TRUE
```

<br/>

**RUBY**

```ruby
str = "string"
num1 = 123
num2 = 123.456
flag = TRUE
```

<br/>

**SCALA**

scala도 javascript처럼 기본적으로 var 키워드를 이용해 변수를 선언한다.

상수를 선언하고자 할 때에는 var 대신 val을 사용하면 된다.

```scala
object HelloWorld {
  def main(args: Array[String]) {
      var str = "string"
      var num1 = 123
      var num2 = 123.456
      var flag = true
  }
}
```


<br/>




