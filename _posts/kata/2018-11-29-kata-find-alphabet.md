---
title: "[kata][python] 알파벳 찾기"
layout: post
tag:
- kata
category: kata
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 알파벳 찾기

출처: <a href="https://www.acmicpc.net/problem/10809" target="_blank">백준 알고리즘 10809번 문제</a>

첫 번째 줄에서 소문자 문자열 S을 받는다.

문자열 S에 알파벳 a부터 z까지가 각각 몇 번째(인덱스)에 등장했는지 공백을 기준으로 출력한다.

```
입력
    backjoon

출력
    1 0 -1 -1 2 -1 -1 -1 -1 4 3 -1 -1 7 5 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1
```    

a부터 z까지 각각의 알파벳이 'backjoon'이라는 문장에서 몇 번째 인덱스에 등장했는지 출력하고있다.

해당 알파벳이 문장내에 없으면 -1을 출력하면 된다.


## 내 풀이

```python
  1 import sys
  2 import string
  3
  4 S = sys.stdin.readline()
  5
  6 for alphabet in string.ascii_lowercase:
  7     print(S.find(alphabet), end=" ")
```

string 모듈의 ascii_lowercase는 소문자 a부터 z까지 문자열이 연속으로 적혀있다.

```python
>>> string.ascii_lowercase
'abcdefghijklmnopqrstuvwxyz'
```

7번째 줄에서 사용한 find 메소드는 문자열에서 해당 알파벳이 존재하는 첫 인덱스 번호를 리턴한다.

문자열에 해당 알파벳이 없으면 -1을 리턴한다.

## 다른사람 풀이

```python
  1 a=[-1]*26
  2 s=input()
  3 for i in s:
  4     if a[ord(i)-97] is -1:
  5         a[ord(i)-97]=s.index(i)
  6 print(''.join(str(e)+' ' for e in a))
```

1번 라인에서 -1이 26개 담긴 리스트를 생성했다.

3번 라인에서 입력받은 문자열의 각 알파벳에 대해 iteration을 시작한다.

4번 라인에서 문자열에 있는 각 알파벳에 ord 함수를 적용해 ascii 코드를 알아내고,

해당 ascii 코드에서 소문자 a의 ascii 코드인 97을 빼서, 1번 라인에서 생성한 리스트 내에서의 위치를 알아낸다.

5번 라인에서 index 메소드를 이용해 문자열에서 알파벳이 처음으로 등장하는 인덱스 번호를 알아내고,

해당 위치에 있는 -1을 해당 인덱스 번호로 대체한다.

마지막으로 6번째 줄에서 join 메소드를 이용해 리스트의 값들을 공백 기준으로 전부 출력하였다.


## 분석

다른 사람의 풀이는 미리 -1이 26개(알파벳 개수)들어간 리스트를 생성해서 문제를 해결했다.

그리고 내 방식과는 달리 모든 소문자에 대해 iteration을 한 것이 아니라,

입력받은 문자열에 있는 알파벳에 대해서만 iteration을 하였다.

하지만 각 iteration마다 if문을 통한 값 비교와 ascii 코드값 분석,

그리고 리스트 값 변경이 일어나서 실제로 어느쪽이 더 효율적일지는 잘 모르겠다.

절대적으로 나은 방법이 있기보다는,

입력받은 문자열의 길이가 길면 내 방식이 효율적일 것 같고,

길이가 짧으면 다른사람 풀이가 더 낫지 않을까 하는 생각이 든다.
