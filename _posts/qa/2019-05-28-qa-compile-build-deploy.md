---
title: "[QA] 컴파일? 빌드? 배포? 개념과 차이는 무엇일까?"
layout: post
tag:
- qa
category: qa
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 컴파일, 빌드, 배포의 개념 및 차이

<br/>

본인이 번역가라고 생각해보자.

이번에 출판사로부터 일을 하나 받았는데,

영문으로된 글을 한글로 번역하는 일이다.

번역된 글은 출판사에서 적절히 페이지를 나누어 책으로 엮을 것이며,

완성된 책은 출판이 되어 서점에 진열될 것이다.

우리는 방금 컴파일, 빌드, 배포의 모든 과정을 훑어보았다.

<br/>

```
1. 영문으로된 글을 한글로 번역하는 것은 컴파일이다.

2. 번역한 글을 책으로 엮는 것은 빌드이다.

3. 완성된 책을 고객들이 읽을 수 있도록 서점에 진열하는 것은 배포이다.

4. 1~2번 과정을 하나로 묶어 '빌드 한다'고 하기도 한다.
```

벽돌과 시멘트등 여러 재료를 사용해 무엇인가를 짓는(build)것의 결과물이 사람이 살 수 있는 집이 되는 것처럼,

코드와 컴파일러등 여러 도구를 사용해 무엇인가를 만드는(build) 것의 결과물은 동작하는 소프트웨어가 된다고 이해하면 좀 더 쉬우려나?

<br/>

즉, 순서대로 보자면 컴파일 - 빌드 - 배포 의 순서이지만,

보통 컴파일을 포함한 배포하기 직전까지의 모든 과정을 '빌드 한다' 라고 표현하기도 한다.

사실 용어를 정확하게 정의해두고 사용하는게 좋겠지만,

실제로 회사나 프로젝트 팀마다 용어를 조금씩 다르게 사용하는 경우가 있으니 참고해두자.

심지어는 코드가 완성된 직후, 컴파일부터 배포하는 모든 과정을 '빌드 한다'고 표현하는 경우도 봤다.

<br/>

어쨌든 이를 좀 더 프로그래밍적 관점에서 보자면,

```
1. 컴파일: 사용자가 작성한 코드를 컴퓨터가 이해할 수 있는 언어로 번역하는 일

2. 빌드: 컴파일된 코드를 실제 실행할 수 있는 상태로 만드는 일

3. 배포: 빌드가 완성된 실행 가능한 파일을 사용자가 접근할 수 있는 환경에 배치시키는 일

4. 혹은 컴파일을 포함해 war, jar 등의 실행 가능한 파일을 뽑아내기까지의 과정을 빌드한다고도 함.
```

<br/>

이클립스에서 JAVA로 코딩을 한다고 생각해보자.

코드를 짜고나서 Run 버튼을 눌러 코드를 실행시킨다 (컴파일 + 실행)

정상적으로 실행되면 이것을 war 파일로 뽑아서(빌드) 웹서버에 올리거나(배포)

JSmooth 등을 사용해 exe, jar 파일로 뽑아(빌드) 사용자에게 주면 된다(배포)

<br/>

참고로, 웹이 아닌 exe 파일로 배포하는 경우는 보통 'deploy'보다는 'distribution' 한다고 표현하는 것 같다.

둘다 똑같은 '배포'이긴 하지만, deploy는 일반적으로 웹개발 영역에서 주로 사용되는 용어로 보인다.

<br/>

어쨌든,

괄호 안에 써놓은 것과 같이 Run 버튼을 누를때 컴파일과 실행이 동시에 발생한다.

때문에 일반적으로 이클립스를 사용하는 경우 컴파일 과정을 인식하기 힘든 부분이 있다.

<br/>

약간 사족같긴 하지만, 말이 나온김에 java를 이클립스가 아닌 터미널에서 직접 실행시켜보자.

다음과 같이 "Hello, World!" 라는 문자열을 출력하는 간단한 코드가 있다.

```java
// HelloWorld.java

public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello, World!");
    }
}
```

이를 터미널에서 실행할 때, 단순히 다음과 같이 실행하면 에러가 발생한다.

```
$ java HelloWorld.java
오류: 기본 클래스 HelloWorld.java을(를) 찾거나 로드할 수 없습니다.
```

아직 내가 작성한 코드가 번역(컴파일)이 되지 않았기 때문에, 컴퓨터가 코드를 이해를 할 수 없기 때문이다.

하지만 이클립스에서는 코드를 작성하고 Run을 누르면 바로 실행이 되었었다.

이는 앞서 말했듯 Run을 누르는 순간 컴파일이 자동으로 이루어지기 때문이다.

터미널에서 직접 실행할 때에는 개발자가 직접 컴파일 작업을 해주어야한다.

```
$ javac HelloWorld.java
$ ls
HelloWorld.class    HelloWorld.java
```

javac 명령을 사용해 파일을 컴파일 해주었더니, 컴파일된 .class 파일이 생겼다.

이제 뒤에 확장자 명을 제외하고 클래스 이름만으로 java 명령어를 실행해보자.

```
$ java HelloWorld
Hello, World!
```

잘 실행이 된다.

만약 누군가 이 파일을 사용하기위해 특정 디렉토리에 위치시켜달라고 요청을 했고,

당신이 그 위치에 파일을 가져다 놓으면, HelloWorld 라는 프로그램을 배포한 셈이 되는것이다.

물론 war 파일이나 exe 파일은 아니지만,

실행가능한 파일을 최종 사용자가 가용한 위치에 옮겨둔다는 개념에서 보면 그렇게 볼 수도 있다는 것이다.

<br/>

실제 서비스를 운영하다보면,

코드를 수정한 이후 다시 컴파일하고 실행가능한 파일로 추출해서 배포하는 과정을 하루에도 몇 번씩 반복해야 하는 경우가 많다.

이러한 반복작업은 매우 귀찮고 실수를 유발하기 쉬운 과정이기때문에, '빌드 자동화', '배포 자동화' 라는 개념이 등장했다.

이 개념들은 공부를 하는대로 다음 포스팅부터 차근차근 다뤄보도록 하겠다.