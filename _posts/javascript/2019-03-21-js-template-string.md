---
title: "[javascript] 템플릿 문자열(template string)"
layout: post
tag:
- javascript
- nodejs
category: javascript
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---


# javascript 템플릿 문자열

템플릿 문자열을 쉽게 설명하자면,

"문자열에 변수를 포함시킬때 좀 더 직관적이고 편하게 사용하기 위한 기능"이다.

무슨 말인지 잘 모르겠으니 예시를 보자.

다음과 같은 코드가 있다.

```javascript
  1 const name = 'lee';
  2 const age = 30;
  3 const address = 'seoul';
  4
  5 const string_introduce = "Hi, My name is " + name + ", " + age + " years old, and I'm living in " + address
  6 
  7 console.log(string_introduce)
```

name, age, address라는 변수를 선언하고,

이를 이용해 자신을 소개하는 문자열을 만들어 출력하는 코드이다.

실행해보자.

```
Hi, My name is lee, 30 years old, and I'm living in seoul
```

정상적으로 동작은 하지만,

5번째 줄의 string\_introduce를 만드는 코드가 뭔가 직관적이지 않고 정신없다.

이 때, 템플릿 문자열 기능을 활용하면 다음과 같이 코드를 개선할 수 있다.

```javascript
  1 const name = 'lee';
  2 const age = 30;
  3 const address = 'seoul';
  4
  5 const string_introduce = `Hi, My name is ${name}, ${age} years old, and I'm living in ${address}`
  6 
  7 console.log(string_introduce)
```

문자열을 만들때 큰따옴표(") 대신 백틱(`)을 사용하고,

변수을 넣고자 하는 부분에 `${}` 키워드를 사용해 그냥 변수를 넣어주면 된다.

문자열을 나눠서 더하기 기호(+)를 통해 연결할 필요가 없기때문에 훨씬 가독성이 좋다.

실행하면 당연히 똑같은 결과가 나온다.

```
Hi, My name is lee, 30 years old, and I'm living in seoul
```

문자열을 생성하는 부분만 떼어서 비교해보면 그 차이가 더 확실히 드러난다.

```javascript
const string_introduce = "Hi, My name is " + name + ", " + age + " years old, and I'm living in " + address
const string_introduce = `Hi, My name is ${name}, ${age} years old, and I'm living in ${address}`
```

하지만 반드시 이렇게 해야 한다는 규칙이 있는것은 아니므로 본인의 취향에 맞는 기능을 선택해서 쓰면 된다.
