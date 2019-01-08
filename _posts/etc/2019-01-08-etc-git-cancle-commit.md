---
title: "git add 취소, git commit 취소, git push 취소"
layout: post
tag:
- etc
- git
category: etc
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# git add, commit, push 취소하기

git에 새로운 내용을 추가할때 보통 add -> commit -> push 순으로 진행된다.

각 단계에서 실수했을때, 이전 단계로 되돌리는 방법을 알아보자.

작업한 파일명은 'Manual-v1.2.md' 라고 하자.

## 1. git add 취소

git add를 실수했을땐 다음과 같이 복구하면 된다.

git add를 취소한다고 변경사항이 사라지는것은 아니니 걱정하지 말자.

```
git reset HEAD Manual-v1.2.md
```

만약 add한 모든 파일을 취소하고 싶다면 인자를 주지 않고 `git reset HEAD` 만 입력하면 된다.

참고로 현재 add된 파일은 git status를 쳤을때 다음과 같이 'Changes to be committed' 목록에 나타난다.

```
# On branch sample-branch
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	new file:   Manual-v1.2.md
#
```

잘 보면 unstage 상태로 돌리기 위해 `git reset HEAD <file>` 명령을 날리라는 설명이 친절하게 되어있다.

unstage라는 용어가 낯설어서 매번 보고도 그냥 지나쳤는데,

레파지토리의 파일에 뭔가 변화가 감지되면 해당 파일은 'unstaged' 상태가 된다. (생성, 수정, 삭제등)

그리고 git add를 하면 파일이 commit되기를 기다리는 상태인 'staged' 상태가 되는 것이고, 

add를 취소한다는 것은 'staged' 상태를 다시 'unstaged' 상태로 돌린다는 뜻이다.

## 2. git commit 취소

git commit 취소는 크게 두 가지 방법으로 할 수 있다.

### A. 작업한 파일들은 그대로 둔 상태로, commit만 취소
```
git reset --soft HEAD^
git reset HEAD^
```

위 두 명령은 둘 다 파일을 그대로 보존한채 commit만 취소한다.

다른점이 있다면, --soft 옵션을 주게 될 경우 staged 상태로 돌아가고, 그렇지 않으면 unstaged 상태로 돌아간다.

즉, --soft옵션을 주면 git add만 한 상태로, 그렇지 않으면 git add를 하기도 이전의 상태로 돌아간다.

참고로 디폴트 옵션은 --mixed로, 두 번째 명령은 이를 생략하여 사용한 것이다.

어쨌든 둘 다 파일이 변경되거나 지워지지는 않으니 걱정하지말자.

### B. commit을 취소하고 작업한 파일도 모두 지우기
```
git reset --hard HEAD^
```

이 명령은 커밋을 돌림과 동시에 변경된 파일들까지 전부 삭제하므로 조심히 사용해야한다.

참고로 뒤에 HEAD^ 대신 commit번호를 입력하면 해당 번호의 commit로 돌아간다.

commit번호는 git log 명령을 쳐보면 나오는 암호같이 생긴 uuid로, 각 commit의 고유값이다.

## 3. git push 취소

push를 실수했을 경우, 이전 상태로 돌리기 위해서는 다음과같이 하면 된다.

```
git reset HEAD^
```

우선 이전 상태로 돌아온 이후에, (마찬가지로 HEAD^대신 돌아가고자 하는 commit 번호를 써도 된다)

다음과 같이 강제로 해당 내용을 브랜치에 적용하면 된다.

```
git push -f origin sample-branch(본인의 브랜치명)
```

수정된 파일은 삭제되지 않고 unstaged상태로 변경된다.
