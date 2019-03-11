---
title: "[linux] 프로세스를 백그라운드/포그라운드에서 실행 및 일시중지하기 (bg, fg, jobs)"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스 백그라운드에서 실행중인 프로세스 관리하기

리눅스에서 동작하는 프로세스는 백그라운드(background)/포그라운드(foreground) 중 하나로 동작한다.

우리가 일반적으로 실행하는 프로그램은 대부분 포그라운드로 실행시키는 것이고,

& 키워드를 사용하면 특정 프로세스를 백그라운드로 동작하게 할 수 있다.

다음과 같이 단순히 10초동안 숫자를 세고 종료되는 python 프로그램이 있다고 하자.

```python
# count_10.py
import time

print("start")
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
print("end")
```

일단 일반적인 방식(foreground)으로 실행해보자.

```
$ python count_10.py
start
end
$
```

프로세스가 실행되는 동안 명령 프롬프트상에서 아무것도 할 수 없다.

만약 포그라운드 실행 중 `CTRL + Z` 를 입력하면, 다음과 같이 프로세스가 일시중지된다.

```
$ python count_10.py
start
^Z
[2]+  Stopped                 python count_10.py
$
```

'end' 가 출력되기 전에 `CTRL + Z`를 눌러 프로세스를 일시중지했다.

jobs 명령을 입력하면 일시중지 해놓은 프로세스를 볼 수 있다.



```
$ jobs
[2]+  Stopped                 python count_10.py
$
```

물론 일시중지 해놓은 프로세스만 출력되는 것은 아니다.

포그라운드/백그라운드에서 실행 및 일시중지중인 프로세스가 있다면 모두 출력된다.

<br/>

일시중지한 프로세스를 다시 실행시킬때, 백그라운드로 실행할지 포그라운드로 실행할지 선택할 수 있다.

`fg 2` 혹은 `bg 2` 를 입력하면 된다.

fg, bg 뒤에 입력하는 숫자는 대괄호 안의 숫자를 입력하면 된다.

혹은 숫자 대신 뒤에 붙은 `+` 혹은 `-` 를 입력해도 된다.

```
$ fg 2
python count_10.py
end
$
```

프로세스가 포그라운드로 재기동되어, 

일시중지 하기 이전의 시점부터 남은 시간을 모두 카운팅 하고 종료되었다.

<br/>

이번에는 & 키워드를 사용해 백그라운드로 실행해보자.

단순히 명령어 뒤에 & 를 붙여주면 된다.

```
$ python count_10.py &
[1] 11634
$ start
$ jobs
[1]+  Running                 python count_10.py &
$ (do something)
$ (do something)
$ end
[1]+  Done                    python count_10.py
```

실행시키면 `[1] 11634`과 같이 `[작업번호] 프로세스ID` 가 출력된다.

그 후 프로세스는 백그라운드에서 알아서 돌아가고, 명령프롬프트를 계속 사용할 수 있다.

jobs라는 명령을 쳐보면, 백그라운드로 동작중인 프로세스가 출력된다. 

<br/>

만약 백그라운드 프로세스를 일시중지하고싶다면,

우선 fg 명령을 통해 포어그라운드로 프로세스를 가져온 다음 `CTRL + Z`를 입력해야한다.

```
$ python count_10.py &
[1] 11634
$ start
$ jobs
[1]+  Running                 python count_10.py &
$ fg 1
python count_10.py
^Z
[1]+  Stopped                 python count_10.py
```

즉, 백그라운드로 실행시킨 프로세스를 일시중지시키는 과정은 다음과 같다.

1. `&` 를 사용해 백그라운드로 실행
2. `jobs` 명령을 사용해 프로세스 번호 알아내기
3. 알아낸 프로세스로 `fg` 명령어를 실행해 포그라운드로 가져오기
4. `CTRL + Z` 명령을 통해 프로세스 일시중지
