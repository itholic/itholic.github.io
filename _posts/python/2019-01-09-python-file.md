---
title: "[python] 파일 읽기, 파일 쓰기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬 파일 다루기

파이썬에서 파일을 읽고 쓰는 방법을 알아보자.

## 파일 읽기

다음과 같은 내용의 test.txt 라는 파일이 있다고 가정하자.

```
hello
world
i
am
python
```

다음과 같이 읽으면 된다.

```python
with open("test.txt") as f:
    contents = f.read()
    print(contents)
```

with 절에 open 메소드를 이용해 파일경로를 입력해주면 된다.

as 뒤에 오는 변수는 해당 파일 객체를 f라는 이름으로 사용하겠다는 의미이다.

그리고 파일객체 f의 메소드인 read()를 이용해 파일 내용 전체를 읽어들여 contents라는 변수에 담아 출력했다.

실행 결과는 다음과 같다.

```
hello
world
i
am
python

```

맨 밑에 개행이 되어있는데, 다음과 같이 rstrip()을 통해 제거해주면 된다.

```python
with open("test.txt") as f:
    contents = f.read().rstrip()
    print(contents)
```

파일을 한 줄씩 읽고싶다면 다음과 같이 readline() 을 사용하면 된다.

```python
with open("test.txt") as f:
    contents = f.readline()
    print(contents)  # hello
```

위 코드는 맨 첫번째 줄인 'hello'만 출력한다.

이번에는 한 줄씩 읽어서 모든 줄을 출력해보자.

```python
with open("test.txt") as f:
    for line in f:
        contents = line.rstrip()
        print(contents)
```

결과는 다음과 같다.

```
hello
world
i
am
python
```

파일 객체는 iterable하다.

따라서 파일 객체를 for문에 넣어 돌리면 파일을 한 줄씩 반환하게된다.

다음과 같이 라인번호를 함께 출력하는 것도 가능하다.

```python
with open("test.txt") as f:
    for i, line in enumerate(f):
        contents = line.rstrip()
        print(i+1, contents)
```

인덱스 번호는 0부터 시작하므로 1을 더해서 프린트해주었다.

실행 결과는 다음과 같다.

```
1 hello
2 world
3 i
4 am
5 python
```

## 파일 쓰기

파일 쓰기는 두 가지 방법이 있다.

기존 내용에 추가하는것과, 새로운 파일을 만드는것.

기존 내용을 추가하려면 파일 오픈시 a 옵션을 주면 된다.

```python
with open("test.txt", "a") as f:
    f.write("bye bye")
```

간단한 예제다.

a 옵션과 함께 파일을 열고, write메소드를 통해 내용을 추가했다.

test.txt 파일을 열어보면 다음과 같이 내용이 추가된 것을 확인 할 수 있다.

```
hello
world
i
am
python
bye bye
```

이번엔 기존 파일을 덮어씌워서 새로운 파일을 만들어보자.

a 옵션대신 w 옵션을 사용하면 된다.

```python
with open("test.txt", "w") as f:
    f.write("bye bye")
```

a 옵션이 w 옵션으로 바뀐 것 외에는 달라진게 없다.

test.txt 파일의 내용은 다음과 같다.

```
bye bye
```

참고로 옵션을 주지 않은 상태에서는 읽기모드로 열리게 된다.

r 옵션을 주어 읽기모드라는 것을 명시할 수도 있다.
