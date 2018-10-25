---
title: "Higher-Order Function(고차 함수)"
layout: post
tag:
- etc
category: blog
author: itholic
sitemap:
  changefreq: weekly
  priority: 1.0
---

# Higher-Order function (고차 함수)

Higer-Order function이란 개념을 처음 보게되었다. 이게 뭘까?

찾아보니 매우 간단한 개념이었다.

지난번에 정리한 <a href="https://itholic.github.io/first-class-citizen/" target="_blank">First-Class citizen(일급 객체)</a> 의 특징을 상기해보자. 

일급 객체의 조건은 

1. 객체를 변수로 할당할 수 있어야 하고,
2. 객체를 함수의 매개변수로 던질 수 있어야하며,
3. 객체를 함수의 리턴값으로 돌려줄 수 있어야한다.

는 것이었다.

그리고 이러한 일급 객체의 특징을 함수가 가지고 있다면, 이를 First-Class function이라고 하는 것 뿐이다.

이 특징 중에서 2번이나 3번의 역할을 하고있는 함수가 있다면, 그것을 고차함수라고 부른다. (;;)

즉, First-Class function을 함수의 매개변수로 던지고있거나, 함수의 리턴값으로 받고있다면 고차함수인 것이다.

```python
def double(num):
    return num * 2

num_list = [1, 2, 3, 4, 5]
doubled_num_list = list(map(double, num_list))

print(doubled_num_list)  # [2, 4, 6, 8, 10]
```

map이라는 함수는 파이썬 내장 함수로써, 함수와 리스트를 매개변수로 받는다.

(예제에서는 double이라는 함수와 숫자 리스트들을 매개변수로 주었다)

그리고 리스트의 값들을 하나씩 꺼내면서 앞의 함수를 적용시키고, 그 결과를 저장해 map 객체로 반환한다.

마지막으로 list 함수를 써서 map 객체를 리스트로 만들어주었다.

말이 어렵지만, 위의 예제를 보면 어느정도 이해가 가능할 것이다.

어쩄든, 이때 double함수는 map이라는 함수의 인자로 넘겨지고 있으므로 고차함수이다.

(앞서 기술한 일급 객체의 조건 세 가지 중 2번째에 해당)
