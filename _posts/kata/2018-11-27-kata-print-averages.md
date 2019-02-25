---
title: "[kata][python] 평균은 넘겠지"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 평균은 넘겠지

출처: <a href="https://www.acmicpc.net/problem/4344" target="_blank">백준 알고리즘 4344번 문제</a>

우선 첫째 줄에서 테스트 케이스의 갯수 N을 받는다.

둘째 줄부터 각 케이스의 학생 점수를 출력하는데,

학생의 수를 맨 처음 적고, 학생의 수 만큼 점수를 적어주면 된다. (0점부터 100사이의 정수)

```
5
5 50 50 70 80 100
7 100 95 90 80 70 60 50
3 70 90 80
3 70 90 81
9 100 99 98 97 96 95 94 93 91
```

그리고 각 테스트 케이스마다 평균을 구하고, 

평균을 넘는 학생의 비율을 반올림하려 소수점 셋째자리까지 출력한다.

```
40.000%
57.143%
33.333%
66.667%
55.556%
```

## 내 풀이

```python
  1 # -*- coding: utf-8 -*-
  2
  3 number_of_test_case = int(input())
  4 over_average_percentage_list = []
  5
  6 for _ in range(number_of_test_case):
  7     input_data_list = input().split(" ")
  8     number_of_student = int(input_data_list[0])
  9     score_list = list(map(int, input_data_list[1:]))
 10
 11     number_of_over_average = 0
 12     for score in score_list:
 13         average = sum(score_list) / number_of_student
 14
 15         if score > average:
 16             number_of_over_average += 1
 17
 18     over_average_percentage = ("{0:.3f}%".format((number_of_over_average / number_of_student) * 100))
 19     over_average_percentage_list.append(over_average_percentage)
 20
 21 for over_average_percentage in over_average_percentage_list:
 22     print (over_average_percentage)
```

우선 3번 라인에서 테스트 케이스의 갯수를 number_of_test_case 변수에 넣었다.

그리고 최종적으로 출력할 '각 테스트 케이스별 평균이 넘는 사람의 비율' 리스트를 over_average_percentage_list 로 정의했다

6번 라인에서 테스트 케이스 갯수만큼 iteration을 했다.

8~10번 라인에서 각 테스트케이스마다 input을 받고, 학생의 수와 점수 리스트를 만들었다.

11번 라인에서 평균을 넘은 사람이 몇명인지 저장할 number_of_over_average를 0으로 초기화하고, iteration에 진입한다.

12~16 라인에서 iteration을 돌며 평균을 구한 후, score가 평균보다 높은 경우 number_of_over_average 값을 1 증가시킨다.

iteration이 끝나면 평균이 넘는 사람의 퍼센테이지를 구하고, over_average_percentage_list에 추가한다.

21~22번 라인에서 iteration을 돌며 각 케이스별 평균이 넘는 비율을 출력한다.

## 다른사람 풀이

```python
  1 import sys
  2 c = int(sys.stdin.readline().rstrip())
  3 for i in range(c):
  4     l = list(map(int, sys.stdin.readline().rstrip().split()))
  5     avg = sum(l[1:])/l[0]
  6     print("{0:.3f}%".format(round((len([j for j in l[1:] if j>avg])/l[0] * 100), 3)))
```

input을 sys.stdin.readline() 으로 받았다.

2번 라인에서 테스트 케이스의 갯수를 받고, 3번라인에서 iteration에 진입했다.

4번 라인에서 입력받은 데이터들을 쪼개서 l 이라는 리스트에 담았다.

5번 라인에서 리스트를 이용해 바로 평균을 구했다.

마지막으로 list comprehension을 활용해 j가 avg보다 큰 경우의 리스트 길이를 구하고,

그것을 입력받은 학생수로 나누어 평균보다 높은 점수를 받은 학생의 비율을 구해 출력했다.

## 분석

다른 사람이 짠 코드고, 짧아졌다고 해서 무조건 더 좋은건 아니지만, 

일단 내가 짠 코드보다 거의 3~4배정도 짧아졌다 (...)

퍼센테이지를 구하는 족족 출력한 것이 아니라, 리스트에 담아뒀다가 마지막에 출력한 부분이 크다.

이는 문제의 예제 출력을 잘못 이해해서 벌어진 사단(?)이다.

그렇다고 해도, 일단 list comprehension을 활용해 코드를 매우 간소화 시켰다는 점이 가장 인상적이다.

그리고 input을 받을때 input() 대신 sys.stdin.readline()을 받은 부분도 인상적이다.

정확한 이유는 더 공부를 해봐야하지만, sys.stdin.readline()을 쓰는 편이 내부적으로 처리가 더 빠르다고한다.

다만 변수명을 한글자 변수로 써서, 코드를 처음보는 사람이 봤을때 의도하는바가 확실히 드러나지는 않는다.

내 코드에서 너무 쓸데없는 거쳐가는 변수가 많다는 생각이 들었다.

최대한 과정을 상세히 기술해야겠다는 강박(?)같은게 있어서 이런 결과가 나온 것 같다.

test case의 갯수, 학생 수, 평균 값 등 프로그램의 핵심적인 변수 외에는 거쳐가는 변수를 최대한 없애서 혼란을 줄이도록 신경써야겠다.
