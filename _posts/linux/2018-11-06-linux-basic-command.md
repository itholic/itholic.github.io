---
title: "[linux] 리눅스 기본 명령어/자주 쓰는 명령어"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 리눅스 기본 명령어

리눅스를 사용할때 숨쉬듯(?) 타이핑하는 기본 명령어들을 정리해봤다.

처음 리눅스를 접하는 사람들에게 조금이나마 도움이 되었으면 좋겠다.

<br/>

모든 명령어는 명령어 뒤에 \-\-help 옵션을 주면 자세한 사용 방법이 나온다.

예를들어 ls 명령어의 자세한 사용 방법과 모든 옵션을 알고싶으면 ls --help를 입력하면 된다.

<br/>

따라서 모든 옵션을 상세하게 다루기보단,

실무를 하며 실제로 자주 사용하는 명령어와 옵션 위주로 그냥 쭉~ 나열해봤다.

물론 그래봤자 이제 2년 남짓한 경력이고, 프로젝트마다 자주 사용하는 명령어와 옵션은 다를 수 있다.


<br/>

### pwd (print working directory)

현재 작업중인 디렉토리 정보 출력

```
# pwd
/home/itholic
```

<br/>

### cd (change directory)

경로 이동

절대 경로와 상대 경로로 이동 가능하다.

절대 경로와 상대 경로에 대해 더 자세히 알고싶다면 <a href="https://itholic.github.io/linux-cd/" target="_blank">해당 포스팅</a> 참조

```
# cd /home/itholic/mydir
# pwd
/home/itholic/mydir


# cd ..
# pwd
/home/itholic
```

<br/>

### ls (list)

디렉토리 목록 확인

```
# ls
testfile1  testfile2  testfile3


# ls -l
total 0
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile1
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile2
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile3


# ls -a
./  ../  testfile1  testfile2  testfile3


# ls -al
total 4
drwxr-xr-x 1 itholic 197121 0 11월  6 22:08 ./
drwxr-xr-x 1 itholic 197121 0 11월  6 22:08 ../
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile1
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile2
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile3
```

<br/>

### cp (copy)

파일 혹은 디렉토리를 복사

디렉토리를 복사할때는 -r 옵션을 주어야함

```
# ls
testdir/  testfile


# cp testfile1 testfile_cp
# ls
testdir/  testfile  testfile_cp


# cp -r testdir testdir_cp
# ls
testdir/  testdir_cp/  testfile  testfile_cp
```

<br/>


### mv (move)

파일 혹은 디렉토리 이동

실제로 원하는 위치로 이동할때도 사용하지만, 이름을 변경하는 용도로도 사용한다.

cp와는 달리 디렉토리를 이동할때도 별다른 옵션이 필요 없다.

```
# ls
testdir/  testfile


# mv testfile testfile_mv
# ls
testdir/  testfile_mv


# mv testfile_mv testdir/
# ls
testdir/


# ls testdir/
testfile
```

<br/>

### mkdir (make directory)

디렉토리 생성

-p 옵션을 주면 하위 디렉토리까지 한 번에 생성 가능

아래 예제중 ls -R 옵션은 디렉토리의 하위목록까지 전부 보여주는 옵션인데,

내 경우 실제로 많이 사용하진 않아서 ls 명령어에서 따로 설명하진 않았다.

mkdir -p 옵션 예제에서 실제로 하위디렉토리가 생성되었다는 것을 보여주기 위해 사용하였다.

```
# ls
testfile


# mkdir testdir
# ls
testdir/  testfile


# mkdir -p a/b/c/d/e/
# ls -R a/
a/:
b/

a/b:
c/

a/b/c:
d/

a/b/c/d:
e/

a/b/c/d/e:

```

<br/>

### rm (remove)

파일이나 디렉토리를 삭제

디렉토리를 삭제할때는 r 옵션을 주어야 한다.

-f 옵션을 주면 사용자에게 삭제 여부를 묻지 않고 바로 삭제한다.

디렉토리를 삭제할 때에는 하위 디렉토리까지 모두 삭제되므로 유의하자.

```
# ls
testdir/  testfile1  testfile2


# rm -f testfile1
# ls
testdir/  testfile2


# rm -rf testdir/
# ls
testfile2
```

<br/>

### touch

파일이나 디렉토리의 최근 업데이트 일자를 현재 시간으로 변경한다.

최근 업데이트 일자는 ls -l 명령을 통해 확인할 수 있다.

아래 예제에서 '11월  6 22:08' 이라고 쓰여진 부분이다.

파일이나 디렉토리가 존재하지 않으면 빈 파일을 만든다.

```
# ls -l
total 0
-rw-r--r-- 1 itholic 197121 0 11월  6 22:08 testfile1


# touch testfile1
# ls -l
total 0
-rw-r--r-- 1 itholic 197121 0 11월  6 22:43 testfile1


# touch testfile2
# ls -l
total 0
-rw-r--r-- 1 itholic 197121 0 11월  6 22:43 testfile1
-rw-r--r-- 1 itholic 197121 0 11월  6 22:44 testfile2
```

<br/>

### cat (concatenate)

cat 명령은 활용 방법이 꽤나 다양하다.

단순히 파일의 내용을 출력할 수도 있고,

파일 여러개를 합쳐서 하나의 파일로 만들 수도 있다.

그리고 기존 한 파일의 내용을 다른 파일에 덧붙일수도 있다.

새로운 파일을 만들때에도 사용된다.

file1, file2, file3 파일에는 각각 간단하게 숫자 1, 2, 3 이 적혀있다.

```
# ls
file1  file2  file3


# cat file1
1


# cat file2
2


# cat file3
3


# cat file1 file2 > file1_2
# ls
file1  file1_2  file2  file3


# cat file1_2
1
2


# cat file1 >> file2
# cat file2
2
1


# cat > file4
hello
world
(작성이 끝나면 ctrl +d 로 파일 저장)


# cat file4
hello
world
```

<br/>

### head

파일의 앞부분을 보고싶은 줄 수만큼 보여준다.

옵션을 지정하지 않으면 파일 상위 10줄을 보여준다.

```
# cat testfile
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15


# head -3 testfile
1
2
3


# head testfile
1
2
3
4
5
6
7
8
9
10
```

<br/>

### tail

파일의 뒷부분을 보고싶은 줄 수만큼 보여준다.

옵션을 지정하지 않으면 파일 하위 10줄을 보여준다.

참고로 -F 옵션을 주고 실행하면,

파일 내용을 화면에 계속 띄워주고 파일이 변하게되면 새로운 업데이트된 내용을 갱신해준다.

주로 실시간으로 내용이 추가되는 로그파일을 모니터링할때 유용하게 사용한다.

```
# cat testfile
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15


# tail -3 testfile
13
14
15


# tail testfile
6
7
8
9
10
11
12
13
14
15


# tail -F testfile
6
7
8
9
10
11
12
13
14
15
(명령어가 종료되지 않고 계속 해당 화면을 출력하며, 파일 내용 변경시 자동으로 갱신해준다)
```

<br/>

### find

특정 파일이나 디렉토리를 검색한다

사용법이 앞의 명령어들에비해 살짝 복잡하므로, 기본 사용법을 언급하자면 다음과 같다.

> find [검색경로] -name [파일명]

파일명은 직접 풀 네임을 입력해도 되지만, * 을 사용해 검색할수도 있다.

나같은 경우 주로 특정 확장자명을 찾기 위해 사용한다.

```
# ls
dir1/  dir3/  file1  file3  picture1.jpg  picture3.jpg
dir2/  dir4/  file2  file4  picture2.jpg  picture4.jpg


# find ./ -name 'file1'
./file1


# find ./ -name "*.jpg"
./picture1.jpg
./picture2.jpg
./picture3.jpg
./picture4.jpg
```

확장자가 .jpg인 파일을 찾았다.

하지만 여기서 그치지 않고, 확장자가 .jpg인 파일만 찾아서 바로 삭제할수도 있다.

exec 옵션을 사용해 다음과 같이 처리하면 된다.

```
# find ./ -name "*.jpg" -exec rm {} \;
# ls
dir1/  dir2/  dir3/  dir4/  file1  file2  file3  file4
```

그리고 다음과 같이 -type 옵션을 주면, 디렉토리나 파일만 지정해서 검색할수도 있다.

```
# find ./ -type d
./
./dir1
./dir2
./dir3
./dir4


# find ./ -type f
./file1
./file2
./file3
./file4
```

다음과 같이 wc -l 옵션과 같이 사용하면,

특정 디렉토리에 find 조건에 맞는 결과 값이 몇개 존재하는지 숫자로 간편히 알아볼 수 있다.


```
# find ./ -type f | wc -l
4
```

지금처럼 파일 갯수가 4개밖에 없을땐 그냥 일일이 세면 되지만, 수백 수천개가 됐을땐 아주 유용하다.

<br/>

마지막으로 아래 내용은 명령어가 조금 복잡하지만, 알아두면 유용해서 적어둔다.

특정 조건에 해당하는 파일들의 내용을 전부 찾아서 바꾸는 것이다.

예를들어 10만개의 파일이 있는데,

그 중에 확장자가 .txt인 파일만 찾아내고,

txt 파일 안에 있는 'hi' 라는 문자열을 'hello'로 바꾸려면 다음과 같이 하면 된다.

```
find ./ -name "*.txt" -exec sed -i 's/hi/hello/g' {} \;
```

짧게 설명하자면,

다음 명령어는 testfile1.txt 이라는 파일의 모든 'hi' 라는 문자열을 'hello'로 바꾸는 역할을 한다.

```
'sed -i 's/hi/hello/g' testfile1.txt
```

이를 find 명령과 조합하여 조건에 맞는 모든 파일에 대해 해당 명령을 수행할 수 있도록 응용한 것이다.
