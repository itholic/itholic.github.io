---
title: "[kata][python] 프로그래머스 - 하샤드 수"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 더 맵게

출처: <a href="https://programmers.co.kr/learn/courses/30/lessons/12947" target="_blank">프로그래머스 - 하샤드 수</a>

## 문제

양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다.

예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다.

자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.


### 제한 사항

x는 1 이상, 10000 이하인 정수입니다.


### 입출력 예

```
arr: 10
return: true

arr: 12
return: true

arr: 11
return: false

arr: 13
return: false
```

### 입출력 예 설명

입출력 예 #1

10의 모든 자릿수의 합은 1입니다. 10은 1로 나누어 떨어지므로 10은 하샤드 수입니다.

<br/>

입출력 예 #2

12의 모든 자릿수의 합은 3입니다. 12는 3으로 나누어 떨어지므로 12는 하샤드 수입니다.

<br/>

입출력 예 #3

11의 모든 자릿수의 합은 2입니다. 11은 2로 나누어 떨어지지 않으므로 11는 하샤드 수가 아닙니다.

<br/>

입출력 예 #4

13의 모든 자릿수의 합은 4입니다. 13은 4로 나누어 떨어지지 않으므로 13은 하샤드 수가 아닙니다.


## 내 풀이

```python
  1 def solution(num):
  2     return True if num % sum(map(int, str(num))) == 0 else False
```

아주 간단한 코드이지만 그래도 설명을 해보자면,

`sum(map(int, str(num)))` 부분을 먼저 살펴보자.

전달받은 num을 우선 string으로 바꾸어서 각 요소를 다시 int로 바꾼 후, 합을 구했다.

전달받은 숫자가 12라면, 우선 `str(num)` 을 통해 '12' 로 바꾸고,

이를 다시 `map(int, '12')` 을 통해 [1, 2] 와 같은 형태로 바꾼 후,

마지막으로 `sum([1, 2])` 와 같이 더해서 3 이라는 결과를 얻은 것이다.

이렇게 하면 각자리 수의 합이 나오고,

마지막으로 `num % 3` 과 같은 식으로 나누어 떨어지는지 확인하면 되는 것이다.

나누어 떨어진다면 하샤드 수이므로 True를, 아니라면 False를 반환하면 된다.


## 단위 테스트

```python
def test_solution1():
    assert solution(10) is True


def test_solution2():
    assert solution(12) is True


def test_solution3():
    assert solution(11) is False


def test_solution4():
    assert solution(13) is False
```

간단한 테스트 코드를 작성해 예제 케이스에 대하여 solution 함수가 제대로 동작하는지 테스트하였다.

단위 테스트는 pytest를 사용했다.


## 분석

단위테스트를 작성하는 습관을 들여보고자 코딩 문제를 풀 때에도 단위테스트를 작성하기 시작했다.

코드를 돌려보고 에러가 나면 그때그때 고치던 것에 비해 좀 더 스스로에게 확신이 생기는(?)듯한 느낌이 든다.

물론 이런 간단한 문제까지 테스트코드를 작성한다면 오히려 생산성을 떨어뜨릴수도 있지만,

생각해보면 실무에서 사용하는 대부분의 함수들은 실제로 그렇게 복잡하지 않다.

그리고 복잡하지 않은 여러 문제들이 모여 복잡해지는 것이라고 생각한다.

그러한 관점에서, 단위 테스트는 복잡한 문제를 다시 단순한 문제로 파편화 시켜주는데 큰 도움을 준다고 생각한다.

정말 실용적인지는 시간이 지나면 알게 될테고, 일단은 꾸준히 연습해봐야겠다!