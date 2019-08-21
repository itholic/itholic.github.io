---
title: "[haskell] 함수-1 (Currying이란?)"
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

# 하스켈 함수1

<br/>

드디어 함수다!

함수형 프로그래밍에서 함수를 배운다고 생각하니 두근거린다.

이번에도 함수형프로그래밍을 이해하기위한 실마리를 조금 더 풀어볼 수 있을까?

공부를 하다보니 왠지 포스팅 한개로 끝나지 않을 것 같아서 제목을 '함수-1'로 정했다.

어쨌든 시작해보자.

<br/>

## Currying

<br/>

함수형 언어에서는 Currying이라는 개념이 중요하다고 한다.

이 개념을 만든 Haskell Curry 의 이름에서 따온것이다.

Currying이 함수형 프로그래밍의 핵심이라고 할만큼 엄청 중요한 개념이라서,

이를 본따 언어의 이름 또한 Haskell로 만들었다고 한다.

(Haskell이라는 언어 자체는 Haskell Curry가 만든게 아니다)

<br/>

어쨌든 Currying이라는 개념 자체는 그렇게 어렵지 않다.

여러 개의 매개변수를 받아 동작하는 함수가 있을 때, (다변수 함수)

한 개의 매개변수를 받아 동작하는 여러 개의 함수로 로직을 분리하는 것이다. (일변수 함수)

<br/>

사실상 개념은 이게 끝이다.

다시 말하지만, 개념 '자체는' 그렇게 어렵지 않다.

하지만 이해한 개념을 실제로 적용하려면 그렇게 쉽지만은 않은 것 같다.

<br/>

### Currying 예시

<br/>

예를들어 두 개의 인자를 받아 더한 값을 리턴하는 plus라는 함수가 있다고하자.

우선 이해를 돕기위해(나도 이해하기 위해...) 파이썬을 사용하겠다.

다변수 함수로 구현하면 다음과 같이 간단하게 구현 가능하다.

```python
def plus(x, y):
    return x + y
```

사용도 편하다.

다음과 같이 사용하면 된다.

```python
plus(2, 3)  # 5
```

<br/>

이제 여기에 Currying을 적용해보자.

다변수 함수의 로직을 일변수 함수 여러개로 분리한다는게 무슨 의미일까?

다음 코드를 보자.

```python
def plus(x):
    return (lambda y: x + y)
```

한 번에 이해하려 하지 말고 일단 보자.

자, 어쨌든 이제 plus 함수는 x라는 변수 한 개만 받아서 실행된다.

그리고 특정한 값을 리턴하는것이 아닌 또다른 함수를 리턴한다.

그 함수는 바로 "lambda y: x + y" 라는 익명함수인데,

y라는 값을 받아서 기존에 받았던 x와 더해주는 익명함수이다.

일단 한 단계만 실행해보자.

```python
plus(2)  # <function plus.<locals>.<lambda> at 0x106f729d8>
```

여기까지만 실행하면 우리는 익명함수를 리턴받게 된다.

좀 더 이해하기 쉽게 표현해 보자면 이런 형태일 것이다.

```python
plus(2)  # (lambda y: 2 + y)
```

plus 2의 결과로 익명함수가 리턴되었고, x는 2인 상태이다.

그럼 이제 익명함수에 y값을 넘겨서 최종 연산 값을 만들어내면 된다.

```python
plus(2)(3)  # 5
```

위 코드가 잘 이해되지 않는다면 다음 코드를 보자.

```python
f = plus(2)  # <function plus.<locals>.<lambda> at 0x106f729d8>
f(3)  # 5
```

이런식으로 plus(2) 라는 함수를 실행한 결과로 f 라는 익명함수가 리턴되었고,

다시 익명함수 f에 인자로 3을 넣어 실행했을때 비로소 2 + 3 의 결과값이 나오는 것이다.

이를 한 번에 이어서 썼기 때문에 plus(2)(3) 과 같은 형태가 나오는 것이다.

<br/>

### 이걸 왜쓰나?

<br/>

그렇다면 plus(2, 3) 과 plus(2)(3)은 뭐가 다를까?

뭐하러 이렇게 복잡하게 할까?

미안하지만 솔직히 나도 100% 이해는 못하겠다.

하지만 최대한 고민을 해보자.

<br/>

먼저, Currying을 사용하지 않은 경우를 생각해보자.

```python
 1  def plus(x, y):
 2      return x + y
 3
 4
 5  plus(2, 3)  # 5 반환, 연산 완료!
```

(line 5) 이 경우, plus(2, 3) 이라는 코드를 실행했을때 인자가 넘어가는순간 바로 연산이 발생한다.

여기서 연산이란, x + y 부분을 말하는 것이다.

한 번에 두 개의 값을 받고, 두 개의 값을 바로 연산해서 리턴한다.

<br/>

이번엔 Currying을 적용한 함수를 생각해보자.

```python
 1  def plus(x):
 2      return (lambda y: x + y)
 3
 4
 5  f = plus(2)  # 익명함수 (lambda y: 2 + y) 반환, y값이 없으므로 아직 연산하지 않음
 6  f(3)  # 5 반환, 연산 완료!
```

(line 5) 이 경우, 연산에 필요한 첫 번째 인자인 2가 들어왔을때는 아직 연산이 발생하지 않는다.

(line 6) 이 부분에서 y에 3이라는 값이 전달되고, 비로소 연산이 발생한다.

**"즉, Currying을 사용하면 함수의 실행을 늦출 수 있다는 장점이 있다"**

물론 함수의 실행을 늦추는것이 항상 장점은 아니다.

하지만 이 장점을 잘 활용한다면 메모리 관리나 성능면에서 매우 우수한 코드를 작성할 수 있다.

빠르다고 유명한 Apache Spark 같은 경우도 Lazy Evaluation의 장점을 극대화한 케이스이다.

<br/>

왜 함수의 실행을 늦추는것이 장점이라고 말하는지 궁금하다면,

<a href="https://itholic.github.io/python-lazy-evaluation/" target="_blank">Lazy Evaluation</a> << 요 포스팅을 참조하면 조금이나마 이해가 될 것이다.

<br/>

### Haskell에서는 어떻게 Currying하나?

<br/>

하스켈 포스팅인데 파이썬 예제만 주구장창 보여준 것 같다.

그렇다면 하스켈에서는 어떻게 Currying을 구현할 수 있을까?

plus라는 함수를 하스켈에서 구현하면 다음과 같다.

```haskell
Prelude> let plus x y = x + y
```

Currying 함수 구현이 끝났다!

<br/>

응? 근데 뭔가 이상한 것 같다.

이렇게되면 다변수 함수가 아닌가?

마치 파이썬에서 다음과 같은 형태랑 똑같아 보인다.

```python
def plus(x, y):
    return x + y
```

하지만 그렇지 않다.

왜냐면,

**"하스켈에서는 기본적으로 모든 함수가 Currying 형태로 동작한다"**

진짜 그런지 확인해볼까?

```haskell
Prelude> let plus x y = x + y
Prelude> plus(2 3)

<interactive>:43:1: error:
    • Non type-variable argument in the constraint: Num (t -> a)
      (Use FlexibleContexts to permit this)
    • When checking the inferred type
        it :: forall a t. (Num a, Num t, Num (t -> a)) => a -> a
Prelude>
```

plus 함수를 선언하고 다변수 함수처럼 사용했더니 에러가 발생한다.

그럼 일변수 함수처럼 일단 한 개의 변수만 넣어보자.

```haskell
Prelude> plus(2)

<interactive>:68:1: error:
    • No instance for (Show (Integer -> Integer))
        arising from a use of ‘print’
        (maybe you haven't applied a function to enough arguments?)
    • In a stmt of an interactive GHCi command: print it
Prelude>
```

plus(2) 까지만 실행한 결과는 특정 값이 아닌 또다른 함수이기 때문에 에러가 발생한다.

그렇다면 파이썬 예제에서처럼 plus(2)로 반환된 함수를 변수에 넣고 사용해보자.

```haskell
Prelude> let f = plus(2)
Prelude> f(3)
5
Prelude>
```

어디서 많이 본 예제같다.

```python
def plus(x):
    return (lambda y: x + y)


f = plus(2)
f(3)
```

위와 같이 파이썬에서 Currying으로 짰던 코드와 형태가 똑같다.

전체 코드를 보자.

편의를 위해 커맨드라인의 'Prelude' 부분을 제외하겠다.

```haskell
plus x y = x + y


f = plus(2)
f(3)
```

만약 Currying 함수의 장점(Lazy Evaluation)을 극대화하고 싶다면,

하스켈의 경우 기본적으로 이를 지원하기때문에 함수 선언이 매우 간결해진다는 장점이 있다.

사실 간결성을 넘어 이러한 구현 방식을 언어 자체에서 사실상 강제하기 때문에,

Currying 함수 작성시에 복잡한 내부 로직을 따로 신경쓰지 않아도 된다는 부분이 더 핵심인 것 같다.

다음엔 보다 복잡하고 실용적인 에제로 Currying의 장점, 함수형 프로그래밍의 장점을 더 알아봐야겠다.

<br/>

+) 추가

참고로, 하스켈에서도 다변수 함수를 만들수 있다.

x, y를 동시에 입력받아 실행하는 다변수 함수는 다음과 같이 정의해주면 된다.

```haskell
plus (x, y) = x + y
```

다음과 같이 사용한다.

```haskell
Prelude> plus (2, 3)
5
```

<br/>

## 정리

<br/>

짧게 정리하자면,

- 함수형 프로그래밍에서는 Currying이라는 핵심 개념이 있다.

- 이는 다변수함수대신 여러 개의 일변수함수를 연결해 최종 연산을 지연시킬 수 있다는 장점이 있다. (Lazy Evaluation)

- 즉, Lazy Evaluation의 장점을 극대화 시키는 애플리케이션을 작성하고싶다면 함수형 프로그래밍이 도움을 줄 수 있다.

<br/>

뭔가 어설프긴 하지만, 우선은 이정도로 정리할 수 있을 것 같다.

아직도 함수형 프로그래밍이 미궁과 같이 복잡하게 느껴지는것은 마찬가지이지만,

그래도 목적지에 도달하기 위해 0.2 걸음 정도는 더 다가간 것 같은 느낌적인 느낌이다!
