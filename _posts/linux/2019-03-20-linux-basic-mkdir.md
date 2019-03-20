---
title: "[linux][basic] mkdir - 디렉토리(폴더) 만들기"
layout: post
tag:
- linux
category: linux
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# mkdir (make directory)

리눅스에서 디렉토리를 생성하려면 `mkdir` 명령을 사용하면 된다.

```
$ mkdir [생성할 디렉토리명]
```

'my\_dir' 이라는 디렉토리를 생성해보자.

```
$ mkdir my_dir
$ ls
my_dir
```

간단히 생성되었다.

이번에는 my\_dir 아래에 하위 디렉토리를 하나 더 만들어보자.

이름은 my\_sub\_dir 로 해보자.

```
$ cd my_dir
$ mkdir my_sub_dir
$ ls
my_sub_dir
```

생성되었다.

그렇다면 my\_dir 과 my\_sub\_dir 을 동시에 생성하려면 어떻게 해야할까?

앞서 만든 디렉토리를 지우고, 이번엔 두 디렉토리를 한 번에 만들어보자.

```
$ rm -r my_dir
$ mkdir my_dir/my_sub_dir
mkdir: my_dir: No such file or directory
```

my\_dir 이 존재하지 않으므로 my\_sub\_dir 도 생성되지 않는다.

이럴때는 -p 옵션을 주면, 상위 디렉토리가 없을 경우 함께 생성해준다.

```
$ mkdir -p my_dir/my_sub_dir
$ ls
my_dir
$ cd my_dir
$ ls
my_sub_dir
```

리눅스에서 디렉토리를 생성하는 방법,

상위 디렉토리부터 하위 디렉토리까지 한 번에 생성하는 방법을 간단히 알아보았다.
