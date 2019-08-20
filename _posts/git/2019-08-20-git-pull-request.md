---
title: "[git] 깃허브 풀 리퀘스트(Pull Request, PR)"
layout: post
tag:
- git
category: git
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# github pull request

<br/>

github에서 PR(Pull Request)의 개념은 중요하다.

핵심은, 내가 작업한 코드가 원본 저장소에 합쳐져도 좋은지 '검토'를 받는 것이다.

혼자 사용하는 레파지토리라면 별 상관 없겠지만,

협업하는 사람이 많아질수록 코드 하나하나를 머지할때 신중을 기해야하기 때문이다.

<br/>

내 로컬에서 잘 돌아간다고해서 바로 원본 저장소에 올리는건 위험한 행동이 될 수 있다.

실제로 서비스중인 환경에서 작동시에는 예상하지 못한 부작용이 발생할 수도 있고,

프로젝트의 코드 컨벤션이 지켜지지 않은 상태라면 다른 사람들의 가독성을 해치고 혼란을 야기할 수 있다.

<br/>

자 그럼 각설하고, 실제로 간단하게 사용해보자.

<br/>

## 1. git 레파지토리 받아오기

<br/>

이 부분은 기본적인 부분이라 스킵할까 하다가,

혹시 처음부터 보는 사람도 있을 수 있으니 간단하게 설명하고 넘어가겠다.

다음 명령을 통해 작업할 git 레파지토리를 받아온다.

```shell
$ git clone <clone url>
```

clone url은 원본 저장소의 우측에 초록색으로 표시된 "Clone or download" 라는 버튼을 눌러 확인할 수 있다.

![main](/assets/images/2019/08/20/git-pull-request/main.png)

<br/>

## 2. 작업 branch 만들기

<br/>

git에서 레파지토리를 clone 했다면,

작업을 하기 전에 나만의 작업 공간을 만들어야한다.

작업을 하는 도중에 만들어도 상관은 없다.

다음과 같은 명령으로 만들 수 있다.

```shell
$ git branch my_branch
```

제대로 만들어졌는지 확인해보자.

```shell
$ git branch
my_branch
* master
```

잘 만들어졌다.

현재 작업중인 브랜치는 앞에 애스터리스크(*) 표시가 붙어있다.

현재는 master 브랜치이므로 방금 생성한 my\_branch로 변경해보자.

```shell
$ git checkout my_branch
$ git branch
* my_branch
master
```

checkout 명령으로 브랜치를 변경하고, 제대로 변경된 것을 확인했다.

참고로 브랜치를 생성함과 동시에 변경하는 것도 가능하다.

```shell
$ git checkout -b my_branch_2
$ git branch
* my_branch_2
my_branch
master
```

checkout에 -b 옵션을 주면, 브랜치 생성과 동시에 해당 브랜치로 이동한다.

이제 열심히 작업하면 된다.

<br/>

## 3. 내 작업 branch에 commit

<br/>

작업을 완료했다면 결과를 원본 저장소에 합치면 된다.

아마 혼자 작업하는 경우에는 보통 다음과 같은 과정으로 코드를 머지했을 것이다.

```shell
$ git add <작업 파일명>
$ git commit -m "[add] testfile"
$ git push origin master
```

일반적인 add - commit - push 과정이다.

중요한건, 마지막의 "origin master" 부분이다.

이 뜻은 원본 저장소(origin)의 master 브랜치에 내 코드를 바로 올리겠다는 뜻이다.

글의 시작에서, 코드를 바로 서비스 브랜치에 머지했을때 발생할 수 있는 문제점에 대해 간단히 언급했다.

(master 브랜치가 서비스중인 브랜치라고 가정한다)

<br/>

그렇다면 이런 상황에서,

바로 master에 커밋하지 않고 나의 작업 내용을 검토받으려면 어떻게 해야할까?

우선 master 브랜치가 아닌 내가 아까 생성한 브랜치에 코드를 커밋한다.

```shell
$ git add <작업 파일명>
$ git commit -m "[add] testfile"
$ git push origin my_branch
```

기존 방식과 전부 똑같고, 다만 push할때 master 부분이 내가 생성한 my\_branch로 변경되었다.

<br/>

## 4. pull request !

<br/>

이제 pull request를 생성하는 일만 남았다!

코드를 커밋하고 웹에서 레파지토리에 접속하면 다음과 같은 화면을 볼 수 있다.

![my_branch](/assets/images/2019/08/20/git-pull-request/my_branch.png)

내가 최근에 my\_branch 라는 곳에서 작업 내용을 push했다는 메시지가 화면에 뜬다.

그리고 우측을 자세히 보면 Compare & pull request 라는 버튼이 있다.

pull request를 하려면 바로 이 버튼을 누르면 된다.

그럼 다음과 같이 내가 원본 브랜치에 합치려는 내용에 대해 간단한 설명을 추가할 수 있는 화면이 나타난다.

![pr](/assets/images/2019/08/20/git-pull-request/pr.png)

나는 그냥 테스트 용이라서 내용 입력을 하지는 않았는데,

일반적으로는 간단히 작업한 내용을 적어주는게 예의(?)이다.

작업 완료 후에는 우측 하단의 "Create pull request" 버튼을 누른다.

<br/>

## 5. 기다리기

<br/>

여기까지 하면 pull request는 모두 끝났다!

이제 작업 내용이 검토를 마치고 머지될때까지 기다리기만 하면 된다.

다음과 같이 코드의 merge 권한이 있는 사람에게는 PR에서 "Merge pull request" 라는 버튼이 뜬다.

![pr_end](/assets/images/2019/08/20/git-pull-request/pr_end.png)

현재 나에게 권한이 있는 레파지토리이기 떄문에 나에게도 해당 PR을 머지할 수 있는 화면이 뜨는데,

이와 같이 다른사람이 올린 PR을 머지할 권한을 가진 사람들을 "커미터(committer)" 라고 부른다.

작업 내용에 문제가 없다면 master 브랜치에 머지를 시켜줄 것이고,

뭔가 문제가 있다면 Comment를 달아 PR 작성자에게 수정을 요청하거나,

Close and comment 버튼을 눌러 PR을 아예 없애버릴수도 있다 (ㅜㅜ)

<br/>

이로써, 간단하게 github에서 pull request 하는 방법을 알아보았다!
