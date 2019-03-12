---
title: "[linux] 리눅스 history"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# history

리눅스에서 history 명령을 사용하면 다음과 같이 여태까지 사용했던 명령어 리스트를 볼 수 있다.

```
  706  ls
  707  wget https://files.pythonhosted.org/packages/45/ae/8a0ad77defb7cc903f09e551d88b443304a9bd6e6f124e75c0fbbf6de8f7/pip-18.1.tar.gz
  708  sudo yum install wget
  709  y
  710  wget https://files.pythonhosted.org/packages/45/ae/8a0ad77defb7cc903f09e551d88b443304a9bd6e6f124e75c0fbbf6de8f7/pip-18.1.tar.gz
  711  sudo yum install wget
  712  wget https://files.pythonhosted.org/packages/45/ae/8a0ad77defb7cc903f09e551d88b443304a9bd6e6f124e75c0fbbf6de8f7/pip-18.1.tar.gz
  713  easy_install pip-18.1.tar.gz
  714  which pip
  715  pip install requests
[itholic@linux ~]$
```

즉, 명령어의 이력을 관리한다는 것인데, 

이를 유용하게 활용할 수 있는 몇가지 방법이 있다.

우선 간단히 `!!` 명령을 치면 바로 직전 명령어를 수행한다.

```
[itholic@linux ~]$ ls
testfile
[itholic@linux ~]$ !!
ls
testfile
```
이를 응용해 `sudo !!` 명령을 사용하면,

이전에 사용했던 명령어를 sudo로 실행할 수 있다.

종종 실수로 sudo를 주지 않고 명령을 실행할떄가 있는데, 이럴떄 재실행하기 용이하다

느낌표 하나만으로 쓸 수 있는 명령도 있다.

맨 처음 수행했던 history목록을 보면 앞에 숫자가 붙어있는것을 볼 수 있다.

```
  706  ls
  707  wget https://files.pythonhosted.org/packages/45/ae/8a0ad77defb7cc903f09e551d88b443304a9bd6e6f124e75c0fbbf6de8f7/pip-18.1.tar.gz
  708  sudo yum install wget
  709  y
  710  wget https://files.pythonhosted.org/packages/45/ae/8a0ad77defb7cc903f09e551d88b443304a9bd6e6f124e75c0fbbf6de8f7/pip-18.1.tar.gz
  711  sudo yum install wget
  712  wget https://files.pythonhosted.org/packages/45/ae/8a0ad77defb7cc903f09e551d88b443304a9bd6e6f124e75c0fbbf6de8f7/pip-18.1.tar.gz
  713  easy_install pip-18.1.tar.gz
  714  which pip
  715  pip install requests
```

느낌표 뒤에 해당하는 숫자를 붙여주면, 해당 명령어를 실행한다.

```
[itholic@linux ~]$ !706
ls
testfile
```

느낌표와 숫자 사이는 붙여서 써야한다.

자주 사용하는 긴 명령어의 history번호를 기억했다가 사용하면 편리하다.

crtl + r 을 누르면 입력창이 (reverse-i-search)` 로 바뀌는데,

이 때 문자를 입력하면 자동으로 history에서 해당 문자와 매치되는 명령어를 찾아준다.

```
(reverse-i-search)`mk': mkdir test_dir
```

ctrl + r을 누르고 g를 눌렀더니 history에서 `mkdir testdir` 이라는 명령어를 찾아줬다.

이대로 엔터를 쳐서 바로 실행할수도 있고, 계속해서 매칭되는 문자열을 입력할수도 있다.

그리고 방향키를 이용해 명령어를 수정한 후 실행할 수도 있다.

<br/>

나만 그런건지 history 관련 명령은 알아도 좀처럼 잘 안쓰게 되던데,

일부러 의식하면서 몇 번 활용하다보니 확실히 편한 느낌을 받아서 자주 사용하는 유용한 몇 가지를 공유한다.
