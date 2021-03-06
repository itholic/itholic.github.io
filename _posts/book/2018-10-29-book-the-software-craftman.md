---
title: "[book] 소프트웨어 장인"
layout: post
tag:
- book
category: book
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 소프트웨어 장인

## 18.10.15

- 코드 공개를 주저하지 말자

<br/>

- 오픈 소스 프로젝트에 기여하며, 뛰어난 개발자들의 습관을 배우자

<br/>

- 블로그에 글을 올려 미약하게나마 지식을 공유하자

<br/>

- 지역 커뮤니티에 참여하자

<br/>

- 페어 프로그래밍을 시도해보자

<br/>

- 프로페셔널로 대우받기 위해서는 프로처럼 행동하자
  
<br/>
  
- 업무 외 시간에도 코딩하자
    
<br/>
    
- 회사에서의 자기계발을 지원하는 것은 의무가 아님. 스스로 자신 커리어의 주인이 되자

<br/>

- 뽀모도로 기법
    - 할 일을 정한다
    - 뽀모도로(타이머)를 25분에 맞춘다
    - 타이머가 끝날때까지 일한다
    - 짧게 쉰다(약 5분)
    - 매 4회의 뽀모도로마다 길게 쉰다 (15~30분)

<br/>

- '아니로' 라고 말할 수 있어야한다. 그것이 오히려 고객과의 신뢰를 지속시키는 방법이다.
    - 영웅이 되려고 하지 말고, 객관적인 상황을 공유하자

<br/>

- 추가적인 코드로 인해 기술적 부채가 더해져서는 안 된다.
    - '나중에 개선해야지'라는 생각은 필요 없다

<br/>

#### **단위 테스트를 작성하는 것 또한 개발의 일부이다. 테스트하지 않았다면 코드가 완성된 것이 아니다**

<br/>

#### **자신이 짠 코드는 자신이 잘 알고있고, 문제가 없을 것이라는 이유로 테스트를 작성하지 않는 개발자는 매우 자기중심적이고 이기적인 사람이다**

<br/>
<br/>

## 18.10.29

- TDD의 비지니스적 가치
    - 테스트코드는 잘 정리된 요구사항과도 같다
    - 따라서, 딱 필요한 만큼만 코딩하도록 유도한다
    - 불필요하게 복잡해지거나 오버엔지니어링 하는 것을 방지한다

<br/>

- 지속적 통합
    - 코드를 올릴때마다 자동으로 전체 테스트 슈트가 실행
    - 테스트가 실패하면 팀원 전체에 이메일 전송
    - 하던 일을 멈추고 마지막 변경점의 버그를 수정하는데 집중
    - 시스템은 항상 배포 가능한 상태로 유지된다
    - 이로인해 QA팀의 부담이 현저히 줄거나, 팀 자체가 필요 없어질 수도 있다

<br/>

- 깨진 유리창 법칙
    - 엉망인 코드가 많을수록 엉망인 코드가 늘어나는 속도도 빠르다
    - 이미 건물이 깨진 유리창이 있다면, 사람들은 그 이상의 유리창이 깨지는 것에 대해서는 무덤덤하다.

<br/>


- 레거시 코드가 있을 때, 전체시스템을 몽땅 뜯어고치려고 하지 말자
    - 현재 수정이 필요한 부분부터 잘 리팩토링 해나가면 된다
    - 몇 년 동안 바뀐적 없는 부분을 굳이 리팩토링 할 필요는 없다
    - 자주 변경되는 부분을 대상으로 시작하면 된다
    - 보이스카웃 규칙은 해당부분을 이해하여 변경할 필요가 있을 때 적용하면 된다


<br/>

- 실행 관례도 하나의 도구일 뿐, 얽매이지 말자
    - 현재 따르는 관례가 있더라도 더 실용적인것이 있다면 언제든 바꿀 준비
    - 검토중인 실행관례가 아무리 좋아도, 현재 시스템에 어떤 가치를 주는지 판단되지 않는다면 도입하지 않는다

<br/>

- 애자일이나 TDD같은 실행관례를 도입하기위한 설득은 어렵다
    - 이를 따르는건 노력과 비용이 수반되고, 익숙해지는데 학습곡선이 필요하다
    - 처음에는 당황스럽고 불편해서 오히려 생산성이 떨어질수도 있다
    - TDD, 연속된 통합, 리팩토링, 페어프로그래밍등의 용어를 사용해 설득하려 들면 어렵다
    - 실제로 어떤 변화를 가져올 수 있을지 예시를 들어 설득한다
    	- ex) 클릭 한 번에 전체 테스트가 가능해지고, 프로그램이 항상 배포 가능한 상태라면 어떻겠습니까?


<br/>

- "어디로 가고 있는지 모른다면, 결국 가고 싶지 않은 곳으로 간다"
    - 커리어를 일종의 몇 년 짜리 프로젝트라고 생각하고, 어떻게 관리할지 고민해보자
    - 소프트웨어 개발과 같이 작은 단위로 나누고, 점진적 반복 작업으로 만든다
    - 작은 작업 단계마다 프로젝트 목표를 재평가하고, 필요한 경우 수정한다

<br/>

- 커리어의 방향을 확신할 수 없을 때에는 모든 문을 두드려본다
    ```
    1. 새로운 것을 공부하고, 기술적 지식을 확장하자.
    2. 지역 커뮤니티에 참석하자.
    3. 다른 개발자들과 교류하자.
    4. 블로깅하자.
    5. 오픈소스 프로젝트에 참여하자.
    6. 프로젝트를 만들어 공개하자.
    7. 컨퍼런스에 참석하자.
    8. 컨퍼런스의 연사로 나서자.
    ```

<br/>

- 지식노동자가 직업을 구할때 따져봐야할 것들
    - 자율성: 무엇을, 언제, 어떻게 등의 조건을 스스로 통제할 수 있는 조건이어야 한다.
    - 통달: 더 나아지기 위해 계속해서 배우고 진화해 나갈 수 있어야 한다.
	- 목적의식: 현재 하는 일에서 가치를 느끼고 생각하며 일


<br/>


#### 역량이 높아질수록 스스로에게 기쁨을 주는 일을 찾기 쉬워진다


