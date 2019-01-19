---
title: "[python] threading - 세마포어(Semaphore)로 쓰레드 제어하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# threading 모듈의 Semaphore로 쓰레드 제어하기

파이썬에서 동시성 프로그래밍을 할 때 사용하는 테크닉은 여러가지가 있다.

그 중 세마포어 개념을 활용해 한 번에 수행할 쓰레드 갯수를 제어하는 방식을 알아보자.

<br/>

다음과 같이 데이터를 복사하는 프로그램을 짠다고 해보자.

source\_csv/ 디렉토리에 있는 100개의 csv 파일을 copied\_csv/ 디렉토리로 복사하고자 한다.

```
$ ls source_csv/
001.csv	007.csv	013.csv	019.csv	025.csv	031.csv	037.csv	043.csv	049.csv	055.csv	061.csv	067.csv	073.csv	079.csv	085.csv	091.csv	097.csv
002.csv	008.csv	014.csv	020.csv	026.csv	032.csv	038.csv	044.csv	050.csv	056.csv	062.csv	068.csv	074.csv	080.csv	086.csv	092.csv	098.csv
003.csv	009.csv	015.csv	021.csv	027.csv	033.csv	039.csv	045.csv	051.csv	057.csv	063.csv	069.csv	075.csv	081.csv	087.csv	093.csv	099.csv
004.csv	010.csv	016.csv	022.csv	028.csv	034.csv	040.csv	046.csv	052.csv	058.csv	064.csv	070.csv	076.csv	082.csv	088.csv	094.csv	100.csv
005.csv	011.csv	017.csv	023.csv	029.csv	035.csv	041.csv	047.csv	053.csv	059.csv	065.csv	071.csv	077.csv	083.csv	089.csv	095.csv
006.csv	012.csv	018.csv	024.csv	030.csv	036.csv	042.csv	048.csv	054.csv	060.csv	066.csv	072.csv	078.csv	084.csv	090.csv	096.csv
```

실제 파일의 내용이 들어있는것이 아니기때문에 눈깜짝할새 복사가 수행되겠지만,

세마포어의 동작을 좀 더 쉽게 이해하기위해 copy를 시작하기 전에 2초간 sleep을 걸어주자.

실제로는 각 파일이 수 GB짜리 대용량 파일이라고 상상해보자.

즉, 다음과 같은 스크립트로 100개의 파일을 copy하려면 약 200초의 시간이 소요된다.

```python
 1 import glob
 2 import time
 3
 4 def copy_from(source):
 5     time.sleep(2)
 6
 7     target = "copied_csv/{}".format(source.split("/")[-1])
 8
 9     print("copy ({})".format(source))
10     with open(source, "r") as rf:
11         with open(target, "w") as wf:
12             wf.write(rf.read())
13
14 def normal_copy(source_path):
15     for source in glob.glob(source_path):
16         copy_from(source)
17
18 if __name__ == "__main__":
19     source_path = "source_csv/*"
20     start = time.time()
21
22     normal_copy(source_path)
23
24     print(time.time() - start)
```

22번 라인에서 normal\_copy 함수를 수행하면,

15번 라인에서 경로에있는 모든 파일을 리스트로 만들어서 다시 copy\_from 함수의 인자로 넣어준다.

copy\_from 함수를 시작하자마자 5번 라인에서 2초간 대기를 한 후, 실제 복사를 수행한다.

수행하면 다음과 같이 실제로 약 200초가 걸리는 것을 확인할 수 있다.

```
copy (source_csv/021.csv)
copy (source_csv/035.csv)
copy (source_csv/009.csv)
copy (source_csv/008.csv)
copy (source_csv/034.csv)

...

copy (source_csv/005.csv)
copy (source_csv/011.csv)
copy (source_csv/010.csv)
copy (source_csv/004.csv)
copy (source_csv/038.csv)

200.291031122
```

한 번에 한 건씩 처리하므로,

함수가 한 번 실행될때 소요되는 시간에 데이터 갯수를 곱한만큼 전체 시간이 소요되었다.

그럼 데이터를 병렬로 처리하면 더 빠르지 않을까?

한 번에 10건씩 처리하려면 어떻게 해야할까?

세마포어를 통해 한 번에 임계영역에 접근할 쓰레드의 갯수를 제어해주면 된다.

다음 코드를 보자.

```python
  1 import threading
  2 import glob
  3 import time
  4
  5
  6 sema = threading.Semaphore(10)
  7
  8 def copy_from(source):
  9     target = "copied_csv/{}".format(source.split("/")[-1])
 10
 11     sema.acquire()
 12     time.sleep(2)
 13
 14     print("copy ({})".format(source))
 15     with open(source, "r") as rf:
 16         with open(target, "w") as wf:
 17             wf.write(rf.read())
 18
 19     sema.release()
 20
 21 def parallel_copy(source_path):
 22     thread_list = [threading.Thread(target=copy_from, args=(source,)) for source in glob.glob(source_path)]
 23
 24     for thread in thread_list:
 25         thread.start()
 26
 27     for thread in thread_list:
 28         thread.join()
 29
 30 if __name__ == "__main__":
 31     source_path = "source_csv/*"
 32     start = time.time()
 33
 34     parallel_copy(source_path)
 35
 36     print(time.time() - start)
```

21번 라인의 normal\_copy 함수를 parallel\_copy 함수로 바꾸었다.

22번 라인에서 경로에있는 모든 파일들을 copy\_from 함수의 인자로 주어 쓰레드 리스트를 생성했다.

그 후 24번 라인에서 리스트에 있는 모든 쓰레드를 수행했다.

<br/>

하지만 한 번에 모든 쓰레드를 수행하지 않고 10개씩 끊어서 수행하기 위해 6번째 줄에 세마포어를 선언했다.

쓰레드가 한 번에 너무 많이 수행되면 시스템에 부하를주어 문제가 발생할 수 있기때문이다.

물론 현재는 내용이 없는 빈 파일로 테스트하는 것이므로 그럴 일은 없지만,

실제로 대용량의 데이터에 대해 수행하는 것이라면 디스크 I/O 부하가 심하게 걸릴 수 있다.

<br/>

하지만 세마포어를 선언만해서는 아무런 의미가 없다.

11번 라인과 19번 라인에서 각각 세마포어를 획득 및 반환하였다.

그리고 그 사이에 실제 실행시킬 코드 영역(임계영역, Critical Section)을 넣어주었다. (12 ~ 18 라인)

임계영역은 한 번에 접근하는 쓰레드를 제어하고자 하는 바로 그 핵심 부분이라고 생각하면 된다.

실제로 실행해보면 다음과 같은 결과를 볼 수 있다.


```
copy (source_csv/003.csv)copy (source_csv/001.csv)
copy (source_csv/028.csv)
copy (source_csv/017.csv)copy (source_csv/016.csv)

...

copy (source_csv/012.csv)
 copy (source_csv/006.csv)
 copy (source_csv/013.csv)
copy (source_csv/007.csv)copy (source_csv/004.csv)copy (source_csv/039.csv)
 copy (source_csv/038.csv)

copy (source_csv/010.csv)copy (source_csv/005.csv)
copy (source_csv/011.csv)

20.0475010872
```

한 번에 여러개의 쓰레드가 프린트를 찍어내서 뭔가 모양이 이상하게 잡혔지만,

최종 수행 시간이 20초로 거의 정확히 10배가 줄어든 것을 확인할 수 있다.

실제로 코드를 돌려보면 10개가 한 번에 출력되고 다시 2초후에 10개가 한번에 출력된다.

참고로 세마포어는 특정 영역에대해 한 번에 접근할 수 있는 쓰레드의 개수를 제어하는 개념이다.

코드를 직접 작성해서 실제 돌아가는 모습을 보면 더욱 확실히 이해할 수 있을것이다.
