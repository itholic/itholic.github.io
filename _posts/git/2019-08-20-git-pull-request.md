---
title: "[git] pull request를 날려 오픈소스에 기여해보자!"
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

깃허브에서 PR(Pull Request)의 개념은 중요하다.

핵심은, 내가 작업한 코드가 원본 저장소에 합쳐져도 좋은지 '검토'를 받는 것이다.

혼자 사용하는 레파지토리라면 별 상관 없겠지만,

협업하는 사람이 많아질수록 코드 하나하나를 머지할때 신중을 기해야하기 때문이다.

<br/>

내 로컬에서 잘 돌아간다고해서 바로 원본 저장소에 올리는건 위험한 행동이 될 수 있다.

실제로 서비스중인 환경에서 작동시에는 예상하지 못한 부작용이 발생할 수도 있고,

프로젝트의 코드 컨벤션이 지켜지지 않은 상태라면 다른 사람들의 가독성을 해치고 혼란을 야기할 수 있다.

<br/>

PR은 다음과 같이 크게 두 가지 방식으로 작성 가능하다.

1. write 권한이 있는 레파지토리의 원본 저장소를 받아 작업후 PR.
  - 예) 내게 write 권한이 있으며, 여러 사람이 작업하는 사내 프로젝트의 경우

2. write 권한이 없는 레파지토리의 fork 저장소를 받아 작업후 PR.
  - 예) 오픈소스처럼 write 권한이 없는 프로젝트에 기여하고 싶을때

<br/>

참고로 두 번째 방식은 write 권한이 있는 레파지토리에서도 당연히 사용 가능하므로,

추후 오픈소스에 컨트리뷰트할 생각이 있다면 이 방식으로 연습하는게 더 나을것이다.

첫 번째 방식은 좀 더 편하고, 두 번째 방식은 더 범용적인 방식이라고 말해두겠다.

(물론 사람에따라 개인차는 있다)

이 글에서는 두 가지 방식 모두 정리할 것이다.

<br/>

## A. 원본 저장소를 바로 clone해서 작업하기

<br/>

저장소를 따로 fork 받지 않고 원본 저장소를 다이렉트로 받아서 작업하는 방식이다.

그리고 앞에서도 말하긴 했지만, 이 경우 PR을 요청할때 write 권한이 있어야한다.

fork에 대해서는 두 번째 방식을 설명할때 같이 설명하도록 하겠다.

바로 시작해보자.

<br/>

### 1. git 레파지토리 받아오기

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

### 2. 작업 branch 만들기

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

현재 작업중인 브랜치는 앞에 애스터리스크(\*) 표시가 붙어있다.

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

### 3. 내 작업 branch에 commit

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

### 4. pull request !

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

### 5. 기다리기

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

## B. 원본 저장소를 fork 받아서 작업하기

<br/>

이번에는 우선 원본 저장소를 fork 받고,

fork받은 저장소에서 작업 후 PR하는 방식이다.

<br/>

fork는 말그대로 포크로 음식을 찍어오듯이,

상대방의 레파지토리를 찍어서 내가 작업 가능한 환경으로 그대로 가져오는것이다.

이렇게 말하면 마치 상대방 레파지토리를 훔쳐오는 것 같은데,

그냥 원본 저장소와 똑같은 복제본을 하나 만든다고 생각하면 된다.

<br/>

나에게 권한이 없는 저장소의 경우,

원본 저장소에 맘대로 수정사항을 반영할 수 없는건 당연하다.

그래서 복제본을 만들어서 그곳에 마음대로 작업한 이후에,

이 작업본이 어때요? 하고 원본 저장소의 주인에게 물어보는 개념이라고 보면 된다.

<br/>

바로 시작해보자.

<br/>

### 1. git 레파지토리 fork 받기

<br/>

fork받는건 정말 쉽다.

실제로 오픈소스에 컨트리뷰트할때 이런식으로 작업하므로, koalas라는 오픈소스를 예제로 가져왔다.

다음과 같이 작업하고자하는 레파지토리에 들어가보면, 우측 상단에 "Fork" 라는 버튼이 있다.

![fork](/assets/images/2019/08/20/git-pull-request/fork.png)

버튼을 누르면 다음과 같이 잠시 로딩화면이 뜬다.

![forking](/assets/images/2019/08/20/git-pull-request/forking.png)

잠깐 기다리면 다음과 같이 포크가 완료된다.

![finish_fork](/assets/images/2019/08/20/git-pull-request/finish_fork.png)

얼핏 보면 원본 저장소처럼 보이지만,

좌측 상단을 보면 개인 계정 밑으로(itholic/koalas) 저장소의 사본이 생성된 것을 확인할 수 있다.

<br/>

**이후의 과정은 첫 번째 방식과 동일하다.**

이 저장소를 clone 받고, branch를 만들고, 작업이 완료되면 push하면 된다.

1~3 까지는 첫 번째 과정과 완전히 같으므로 해당 내용을 참고하면 된다.

<br/>

### 2. pull request!

<br/>

사실 PR을 생성하는 부분도 다를바는 없다.

하지만 약~~간 다른 부분이 있어서 설명을 위해 절차를 넣었다.

<br/>

포크한 저장소에서 작업을 한 다음 변경사항을 커밋하면 다음과 같이 PR 버튼이 활성화된다.

![pr_fokred](/assets/images/2019/08/20/git-pull-request/pr_fokred.png)

여기까지는 처음 방식과 똑같다.

좌측 상단을 보면 알겠지만, 현재 위치는 원본 저장소가 아닌 포크받은 나만의 저장소이다.

하지만 Compare & pull request 버튼을 누르면 다음과 같이 원본 저장소로 PR 요청을 생성하게된다.

![pr_origin](/assets/images/2019/08/20/git-pull-request/pr_origin.png)

좌측 상단을 보면 "itholic" 이었던 부분이 다시 원본 저장소인 "databricks"로 변경된 것을 확인할 수 있다.

자세히보면 itholic/koalas의 hjlee 브랜치에서 **itholic**/koalas의 master 브랜치로 머지하는것이 아니라,

itholic/koalas의 hjlee 브랜치에서 바로 **databricks**/koalas의 master 브랜치로 머지를 요청하고있다.

<br/>

즉, 개인 레파지토리에 PR을 요청하는 것이 아닌 원본 저장소에 PR을 요청하는 것이므로,

오픈소스에 컨트리뷰트할 경우(PR을 요청할 경우)에는 이 시점에서 작업 내용에 대한 PR코멘트를 성의있게 작성해야한다.

이후에 기다리는 과정은 동일하다.

<br/>

## 3. upstream 설정하기

<br/>

기본적인 PR 생성에 관련된 설명은 끝났고, 이는 부가설명이다.

upstream 설정은 원본 저장소(databricks/koalas)와 fork 저장소(itholic/koalas)를 동기화하기 위한 작업이라고 보면 된다.

<br/>

원본 저장소를 fork로 가져와서 작업할 경우,

현재 내가 작업중인 브랜치는 원본이 아닌 복제본이다.

그리고 원본 저장소에는 누가, 언제 코드를 변경할지 모른다.

만약 변경사항이 있다면, 현재 내가 작업중인 복제본에도 이 부분을 반영해야 할 것이다.

<br/>

하지만 fork를해서 복제본을 만든 경우,

현재로써는 원본 저장소의 위치를 알 수 없다.

git remote 명령으로 원격 저장소들의 목록을 확인해보자.

```
$ git remote -v
origin	https://github.com/itholic/koalas.git (fetch)
origin	https://github.com/itholic/koalas.git (push)
```

현재 원본 저장소는 ~databricks/koalas.git 인데,

내가 fork한 복제본인 ~itholic/koalas.git 밖에 인식하지 못한다.

<br/>

원격 저장소의 위치를 인식할 수 있도록 등록을 해주면 된다.

git remote add 명령어 뒤에 원본 저장소의 별칭과 git url을 적어주면 된다.

```shell
$ git remote add upstream https://github.com/databricks/koalas.git
```

참고로 "upstream" 부분은 본인이 원하는 임의의 별칭을 사용해도 상관없다.

하지만 관습적으로 원본 저장소에 대한 별칭으로 "upstream"이라는 키워드를 사용한다고 한다.

다시 git remote 명령으로 제대로 등록이 되었는지 확인해보자.

```shell
$ git remote -v
origin	https://github.com/itholic/koalas.git (fetch)
origin	https://github.com/itholic/koalas.git (push)
upstream	https://github.com/databricks/koalas.git (fetch)
upstream	https://github.com/databricks/koalas.git (push)
```

upstream이라는 이름으로 등록된 원본 저장소(databricks/koalas)를 확인할 수 있다.

근데 origin에 해당하는 동일한 url이 두 개가 있고, upstream또한 그렇다.

잘 보면 (fetch) 와 (push)로 나뉘어지는데, fetch는 읽기, push는 쓰기라고 보면 된다.

즉, 위 네 줄의 출력 결과가 순서대로 의미하는 바는 각각 다음과 같다.

1. origin이라는 별칭으로 읽기(fetch) 작업을 할때 어떤 저장소를 읽을 것인지 보여준다. (보다시피 itholic/koalas 즉, 복제본)

2. origin이라는 별칭으로 쓰기(push) 작업을 할때 어떤 저장소에 쓸 것인지 보여준다. (마찬가지로 복제본)

3. upstream 이라는 별칭으로 읽기(fetch) 작업을 할때 어떤 저장소를 읽을 것인지 보여준다. (보다시피 databricks/koalas 즉, 원본)

4. upstream 이라는 별칭으로 쓰기(push) 작업을 할때 어떤 저장소에 쓸 것인지 보여준다. (마찬가지로 원본)

이제 원본 저장소의 최신 버전을 읽어오려면 어떤 명령을 수행해야할지 감이 잡힌다.

3번째 줄의 내용을 참고해, "upstream"이라는 별칭(원본)으로 "fetch" 작업(읽기)을 하면 될 것이다.

즉, 원본 저장소와 현재 내 저장소를 동기화시키고싶다면 다음과 같이 명령하면 된다.

```shell
$ git fetch upstream
remote: Enumerating objects: 21, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 11 (delta 10), reused 5 (delta 5), pack-reused 0
Unpacking objects: 100% (11/11), done.
From https://github.com/databricks/koalas
 * [new branch]      master     -> upstream/master
$
```

<br/>

참고로 fetch가 아닌 pull 명령으로도 코드를 가져올 수 있는데,

이 두 명령어의 차이는 따로 포스팅하도록 하겠다.

<br/>

이로써, 간단하게 github에서 PR을 생성하는 두 가지 방법을 알아보았다.

이제 우리는 언제든 오픈소스에 기여(contribution)할 수 있게되었다.

오픈소스에 기여하는것은 생각보다 어렵지 않다. (그렇다고 생각보다 쉽지도 않다…ㅎㅎ)

심심할때 오타 하나라도 고쳐서 PR을 한 번 날려보자!
