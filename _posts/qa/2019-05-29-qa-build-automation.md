---
title: "[QA] 빌드 자동화, 배포 자동화, 테스트 자동화"
layout: post
tag:
- qa
category: qa
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 빌드 자동화, 배포 자동화, 테스트 자동화

<br/>

<a href="https://itholic.github.io/qa-compile-build-deploy/" target="_blank">앞선 포스팅</a>에서 컴파일, 빌드, 배포의 개념에 대해 알아보았다.

이번에는 이러한 일련의 과정을 '자동화한다'는 것이 무엇을 의미하는지에 대해 다루어보려한다.

나또한 이제 막 공부를 시작하는 과정이기에 최대한 필터링하며 읽는 것을 권장한다.

<br/>

## 반복되는 작업들

<br/>

완성된 코드를 서버에 올린다고 개발이 끝나는것이 아니다.

오히려 진짜 개발자의 일은 서비스 론칭 이후 부터 시작이라고봐도 과언이 아니다.

<br/>

서비스를 시작한 이후에는 무수한 버그와 개선사항이 등장할 것이며,

코드의 수정이 있을때마다 컴파일, 빌드, 배포등의 과정이 반복되어야한다.

<br/>

이러한 과정들을 코드의 수정이 있을때마다 사람이 직접 수행하는것은 꽤나 비효율 적이며,

각 과정을 수작업으로 진행하는 부분에서 실수를 유발하기 쉽다.

<br/>

서비스중인 프로그램의 코드를 변경한다고 생각해보자.

수정된 코드를 git에 올리고, 통합된 코드를 다시 컴파일하고 빌드해 배포하는 등의 과정이 필요하다.

<br/>

좀 더 나아가 생각해보면,

코드가 제대로 동작하는지 테스트 코드를 작성하고, 이를 수행 및 검증하는 작업도 필요할 것이다.

<br/>

하지만 앞서 말했듯,

이러한 과정들은 대개 사람이 직접 수행할 필요가 없는 반복 작업들이다.

오히려 사람이 수행했을때 실수를 유발할 가능성이 더 높다.

<br/>

## 자동화

<br/>

이렇게 되면 어떨까?

개발자는 단순히 git에 수정된 코드를 올리기만하고,

컴파일, 테스트, 빌드, 배포 등의 과정은 정해진 절차에따라 특정 프로그램이 자동으로 수행하는 것이다.

git에 코드를 올리는 행위 자체가 트리거가되어 나머지 과정은 자동으로 수행된다고 생각하면 된다.

그리고 모든 과정이 끝나면 그 결과를 개발자에게 리포트 해준다.

<br/>

사람이 직접 수행할 필요가 없는 부분을 프로그램이 대신 자동으로 수행해 주는 것,

말그대로 이것이 자동화이다.

그리고 수많은 절차중 어떤 절차를 자동화하느냐에 따라 '빌드 자동화', '배포 자동화', '테스트 자동화' 라는 용어가 붙는 것 뿐이다.

<br/>

즉, 빌드 자동화, 배포 자동화, 테스트 자동화는 어려운 용어가 아니다.

어떤 프로그램을 서비스하기 위해 당연히 빌드, 테스트, 배포 등 일련의 과정이 필요하며,

이 중 반복되는 작업을 '자동으로 돌아가게' 하고자 하는 필요성에 의해 나온 용어일 뿐이다.

<br/>

일련의 과정 중 빌드를 하는 부분을 자동화 시킨다면 그것은 빌드 자동화이고,

배포하는 부분을 자동화 시킨다면 배포 자동화,

테스트 절차를 자동화 시킨다면 테스트 자동화가 되는 것이다.

<br/>

다음으로는 해당 포스팅의 연장선인 CI/CD에 대해 설명하고자 한다.

원래 한 개의 포스팅으로 작성했었는데,

내용이 너무 길어져 지루한 감이 있어서 두 개로 나누었다.

아래 링크를 달아두었다.

<a href="https://itholic.github.io/qa-cicd/" target="_blank">CI/CD 란?</a>
