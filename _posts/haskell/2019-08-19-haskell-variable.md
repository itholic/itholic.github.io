---
title: "[haskell] 변수 (함수형 프로그래밍 불변성, 동시성)"
layout: post
tag:
- haskell
- functional
category: haskell
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 하스켈 변수

<br/>

하스켈에서 변수는 우리가 알던 그 변수랑 좀 다르다.

예제를 보자.

우선 다음과 같이 변수를 선언해준다.

```haskell
-- variables.hs
x = 10
```

variables.hs 라는 파일을 만들어서 x = 10 이라는 변수를 선언했다.

ghci에서 불러와보자.

```haskell
[kdc@kdc haskell]$ ghci
GHCi, version 7.6.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude> :load variables.hs
[1 of 1] Compiling Main             ( variables.hs, interpreted )
Ok, modules loaded: Main.
*Main> x
10
*Main>
```

:load 를 통해 불러오고 x 를 출력해봤더니 값이 잘 나온다.

x 를 통해 연산도 가능할까?

```haskell
*Main> x + 10
20
*Main> 
```

가능하다.

<br/>

그럼 우리가 알던 변수가 뭐가 다르다는건가?

다음과 같이 변수를 선언하고 변경해보자.

```haskell
-- variables.hs
x = 10
x = 20
```

<br/>

x에 10을 할당한 이후, 20으로 값을 변경했다.

ghci에서 이 파일을 불러오면 다음과 같은 에러가 발생한다.

```haskell
Prelude> :load variables.hs
[1 of 1] Compiling Main             ( variables.hs, interpreted )

variables.hs:2:1:
    Multiple declarations of `x'
    Declared at: variables.hs:1:1
                 variables.hs:2:1
Failed, modules loaded: none.
Prelude>
```

"Multiple declarations of `x'" 라는 에러가 발생한다.

**즉, 한 번 선언된 변수는 그 값을 변경할 수 없다.**

<br/>

## 불변성!

<br/>

아하.

이게 바로 함수형 프로그래밍을 이론적으로 공부할때 지겹도록 강조하던 불변성(Immutable)인가보다.

이제 어떤 위치에서건 x의 값은 10으로 고정되어 있다.

따라서 x를 매개변수로 받아 연산을 수행하는 특정 함수에 대하여,

그 함수는 항상 같은 값을 출력하리라 기대할 수 있겠다.

x의 값은 절대로 변경되지 않기 때문이다!

<br/>

## 동시성!

<br/>

또 이렇게도 생각해 볼 수 있겠다.

어떤 함수가 매개변수로 받은 x를 가지고 뭔가 쪼물딱(?)거리는동안,

그 누구도 중간에 x의 값을 바꿀 수 없다.

<br/>

그렇다면 이런걸 유추해 볼 수 있다.

동일 변수에 대해 다수의 쓰레드가 동시에 접근하는 상황에서,

각 쓰레드는 각자 자신이 원하는 결과를 안전하게 얻어낼 수 있을것이다.

여러 쓰레드가 공유하는 변수에 대해, 특정 쓰레드가 절대로 그 값을 변경할 수 없기 때문이다.

<br/>

결국 함수형 프로그래밍에서 동시성이란,

불변성이라는 성질에 의해 자연스레 파생될 수 밖에 없는 특징이 아니었나 싶다.

<br/>

## !주의!

<br/>

글쎄, 어느정도는 일련의 추측들이 맞지 않을까 생각하지만,

한 편으로는 완전히 틀린 헛소리를 하고있는 것일 수 있으므로 주의하자.

나또한 하스켈을 완전히 처음 접한 초짜이고,

함수형 프로그래밍이라는 미궁을 돌파하기 위해 하스켈이라는 실타래를 조금씩 풀며 길을 찾고있을 뿐이다.

옳다고 생각했던 방향의 끝에 막다른길이 있을 수 있지만, 실타래를 잘 풀어놓았다면 다시 돌아올 수 있으니까!

<br/>

어쨌든 헛소리는 여기까지하고.

꾸준히 실타래를 풀어나가며 미궁속으로 더욱 깊숙히 들어가보자.