---
title: "[haskell] hello, 함수형 프로그래밍"
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

# 함수형 프로그래밍

<br/>

시작하기 전에 미리 말해두겠다.

사실 이 글은 제목과 달리 함수형 프로그래밍이 무엇인지에 대해 제대로 설명하고 있지 않다.

다만 이 글을 기점으로 함수형 프로그래밍이 무엇인지 하나하나 학습해 나갈 생각이다.

그러니 당장 이 글을 통해 함수형 프로그래밍을 이해할 생각이었다면 뒤로가기를 누르는게 현명하다.

<br/>

그럼 각설하고, 시작하겠다.

함수형 프로그래밍이란,

1. 순수 함수를 조합해 부작용을 최소화하는 프로그램을 지향하는 패러다임이란다.

2. 불변의 값들을 사용해 동시성 작업을 좀 더 안전하게 구현할 수 있단다.

3. 보다 직관적인 코딩이 가능하여 가독성을 높이고 로직에 몰입할 수 있단다.

<br/>

그러니까...

이게 또 무슨 특정 언어에 국한된 것이 아니라 사고방식을 전환하는 개념이란다.

기존의 방식과는 다른... 로직을 설계하는 시각이 바뀌고... 새로운 세상이 보이고...

이런, 망할.

내 멍청한 대가리는 여기까지가 한계라고 말한다.

<br/>

그래서 그냥 하스켈을 써보기로 했다.

이런 저런 글들을 읽어보면,

하스켈은 모든 부작용을 극단적으로 증오하고, 그것을 통제하기 위해 노력하고있단다.

즉, 함수형 프로그래밍 그 자체라는 듯한 뉘앙스로 이야기하고 있기 때문이다.

<br/>

솔직히 이것도 뭔소리인지 감이 아예 안오고.

그냥 쓰다보면 조금씩 이해가 되고, 다시 저것들을 읽어보면 무슨 말인지 감이 잡히지 않을까.

하스켈로 실제 프로그램을 짜지는 않더라도,

하스켈을 통해 배운 함수형프로그래밍 패러다임 자체는 분명 언젠가 도움이 될 것 같은 느낌이 든다.

<br/>

## 하스켈 설치

<br/>

그래서 일단 닥치고 깔아봤다.

참고로 나는 centos7 에서 했다.

'haskell' 로 입력하니 설치가 안돼서 찾아보니 'haskell-platform'으로 설치하면 된단다.

```shell
$ sudo yum install haskell-platform
```

<br/>

설치했으니까 실행해보자.

쉘에서 'ghci' 명령을 입력하고 명령줄이 'Prelude'로 바뀌면 된다.

```haskell
$ ghci
GHCi, version 7.6.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude>
```

참고로 ghc는 'Glasgow Haskell Compiler' 의 약자이고,

i는 ghc의 interactive 환경 정도로 이해하면 된다.

<br/>

실행했으면 뭐다?

hello world를 찍어보자.

```haskell
Prelude> putStrLn "Hello, World!"
Hello, World!
Prelude>
```

'putStrLn' 은 문자열을 프린트 해주고 한 줄 개행해주는 함수이다.

'putStr' 까지만 쓰면 개행은 하지 않는다.

<br/>

문자열이 아닌 숫자를 써봤더니 다음과 같이 안된다고 발광을한다.

```haskell
Prelude> putStrLn 1

<interactive>:61:10:
    No instance for (Num String) arising from the literal `1'
    Possible fix: add an instance declaration for (Num String)
    In the first argument of `putStrLn', namely `1'
    In the expression: putStrLn 1
    In an equation for `it': it = putStrLn 1
Prelude>

```

<br/>

## 함수 선언

<br/>

일단 마무리하고 다음 글에서 계속 정리할까 하다가,

명색이 '함수형' 프로그래밍 공부를 시작했는데 함수 한 개 정도는 선언을 해봐야겠다고 생각했다.

<br/>

숫자를 받아서 두 배로 뻥튀기해주는 doubler 라는 함수를 만들어보자.

```haskell
Prelude> let doubler x = x * 2
```

마치 변수를 선언하는 것 처럼 '=' 을 이용해 함수를 정의한다.

대충 모양을 보면 어떻게 만들어졌는지 이해가 될거다.

doubler라는 녀석은 x 라는 매개변수를 받아서 동작하고,

그 x 라는 매개변수에 2를 곱한 값을 리턴해주는 함수이다.

<br/>

잘 동작할까?

```haskell
Prelude> doubler(10)
20
```

그렇다.

괄호를 생략하고 동작시킬 수도 있다.

```haskell
Prelude> doubler 10
20
```

<br/>

참고로 함수를 파일에 정의한 다음 ghci에서 불러올수도 있다.

무슨말이냐면.

```haskell
-- function_test.hs
doubler x = x * 2
```

일단 이런식으로 'function_test.hs' 라는 파일에 함수를 선언한다.

이 때는 커맨드라인에서와는 달리 'let' 키워드를 생략해야한다.

<br/>

그리고 다음과 같이 ghci를 실행할때 파일명을 입력해주거나

```haskell
$ ghci function_test.hs
GHCi, version 7.6.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
[1 of 1] Compiling Main             ( test.hs, interpreted )
Ok, modules loaded: Main.
*Main> doubler(200)
400
*Main>
```

<br/>

아니면 그냥 실행 후에 ':load' 명령을 사용해서 파일을 불러와도 된다.

```haskell
$ ghci
GHCi, version 7.6.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude> :load function_test.hs
[1 of 1] Compiling Main             ( test.hs, interpreted )
Ok, modules loaded: Main.
*Main> doubler(200)
400
*Main>
```

스크립트에 작성해놓은 doubler 함수가 잘 동작한다.

이제 다음 포스팅부터는 하스켈을 좀 더 파보면서 함수형 프로그래밍이란 무엇인지 한 걸음 더 다가가보자.