---
layout: post
title:  "객체지향의 사실과 오해"
author: "이희수"
---

*객체지향의 사실과 오해 - 조용호 저*를 요약한 글입니다.

# 협력하는 객체들의 공동체

## "실세계의 모방" 객체지향에 대한 오해. 

"객체지향이란 실세계를 직접적이고 직관적으로 모델링할 수 있는 패러다임"은 객체지향의 세계에 입문하게되면 가장 먼저 마주하게 되는 설명이다. 많은 책에서 객체지향 프로그래밍은 실세계를 유사하게 모방하여, 소프트웨어 내부로 옮겨 오는 것이라고 설명한다. 하지만 실제 어플리케이션 개발에 뛰어들 때, 실세계의 모방이라는 개념을 갖고 코드를 작성하려고 할 때 이 개념은 혼란을 만들어 낸다. 많은 경우 객체와 실세계의 사물 간의 개념적 거리는 유사성을 찾기 어려울 정도록 매우 멀기 때문이다. 예를 들어 화재를 막는 방화벽과 네트워크 방화벽의 유사성을 곱씹어 생각해보면, 이 둘은 사실 연관성이 적다.

**객체지향의 목표는 세계를 모방하는 것이 아니고 새롭게 창조하는 것이다.** 노련한 객체지향 전문가들은 이런 사실을 인지하고 있다.

실세계의 모방이라는 개념은 실용적이지 않지만, 객체지향을 이해하고 학습하는데 효과적이다.


## 협력하는 사람들 : 객체지향에서 역할, 책임, 협력

```
카페에서 손님이 커피를 먹기 까지.

손님이 캐셔에게 커피를 주문한다.
캐셔는 주문을 받는다.
바리스타는 커피를 제조한다.
제조된 커피를 전달받은 캐셔가 손님에게 커피를 전달한다.
```

모든 음료 주문은 손님이 커피를 주문하고, 캐셔가 주문을 받고, 바리스타가 커피를 제조하는 과정을 거쳐야 완료된다. 이 과정은 역할, 책임, 협력이라는 일상 속에 항상 스며들어 있는 세 가지 개념이 한데 어울려 조화를 이루며 만들어 낸 것이다. 모든 과정 속에는 손님, 캐셔, 바리스타 사이의 암묵적인 **협력** 관계가 존재한다. 손님은 주문을 하는 역할, 캐셔는 주문을 받는 역할, 바리스타는 커피를 제조하는 역할을 맡고있다. 그리고 각자가 맡은 역할을 책임지고 수행한다. *커피 주문* 이라는 **협력**에 참여하는 사람들은 커피가 정확하게 주문되고 주문된 커피가 손님에게 정확하게 전달될 수 있도록 **역할**과 **책임**을 다하고 있는 것이다. 그리고 참여한 사람은 각자에게 *요청*하고 *응답*하면서 **협력**하여 커피 주문의 과정을 완성한다.

## 역할과 책임

**역할**은 어떤 협력에 참여하는 특정한 사람이 협력 안에서 차지하는 책임이나 임무를 의미한다. 손님은 주문을 해야하고, 바리스타는 커피를 제조해야 한다.

위 정의에서 역할이라는 개념이 **책임**이라는 개념을 포함하고 있다. 선생님이라는 역할을 학생을 가르칠 책임이 있음을 암시한다. 이처럼 특정한 역할은 특정한 책임을 암시한다.협력에 참여하며 특정한 역할을 수행하는 사람은 역할에 적합한 책임을 수행하게 된다. *역할과 책임은 협력이 원활하게 진행 되는 데 필요한 핵심 구성요소다.*

역할과 책임은 상식적으로, 아래의 특징을 갖고 있다.

* 여러 사람이 동일한 역할을 수행할 수 있다.
* 그래서 역할은 대체 가능성을 의미한다. 예를 들어 오전에 캐셔를 보던 사람은 퇴근하고, 이어서 오후에 출근한 사람이 캐셔 역할을 수행할 수 있다.
* 책임을 수행하는 방법은 자율적으로 선택할 수 있다. 바리스타는 커피를 제조하는 역할을 자신만의 방법으로 독트한 커피를 제조 할 수 있다.
* 한 사람이 동시에 여려 역할을 수행할 수 있다. 예를 들어 작은 카페에서는 사장이 캐셔와 바리스타 역할을 동시에 수행한다.

## 역할, 책임, 협력

#### 기능을 구현하기 위해 협력하는 객체들
#### 역할과 책임을 수행하며 협력하는 객체들

"커피 주문"에서 사람을 객체로, 에이전트의 요청을 메시지로, 에이전트가 요청을 처리하는 방법을 메서드로 바꾸면, 자연스럽게 객체지향 세계에서의 역할, 책임, 협력의 개념을 설명할 수 있다.

사람들은 커피 주문과 같은 특정한 목표를 이루기 위해 서로 협력한다. 협력의 핵심은 특정한 책임을 수행하는 역할들 간의 연쇄적인 요청과 응답을 통해 목표를 달성한다는 것이다.

목표는 책임으로 분할되고, 책임을 수행할 수 있는, 적절한 역할이 할당된 사람에 의해 수행된다.

협력에 참여하는 각 개인은 책임을 수행하기 위해 다른 사람에게 도움을 요청하기도 하며, 이를 통해 연쇄적인 요청과 응답으로 구성되는 협력관계가 완성된다.

비슷하게 소프트웨어에서 어플리케이션의 기능은 더 작은 책임으로 분할되고 책임은 적절한 역할을 수행할 수 있는 객체에 의해 수행된다. 객체는 자신의 책임을 수행하는 도중에 다른 객체에게 도움을 요청하기도 한다. 결론적으로 어플리케이션은 역할과 책임을 수행하는 객체의 협력(요청과 응답)으로 구현된다.

객체의 역할은 사람의 역할과 유사하게 다음과 같은 특징을 지닌다.

* 여러 사람이 동일한 역할을 수행할 수 있다.
* 역할은 대체 가능성을 의미한다.
* 책임을 수행하는 방법은 자율적으로 선택할 수 있다.
* 한 사람이 동시에 여려 역할을 수행할 수 있다.

(Java에서 인터페이스의 개념과 활용에서 이런 특징을 찾을 수 있다. 반드시 인터페이스를 사용해야 역할이라는 개념을 구성할 수 있는 것은 아니다. 다형성도 이런 역할의 특징과 관련이 있어 보인다.)

## 협력 속에 사는 객체

협력에 참여하는 주체는 객체다. 협력 공동체 속에서 객체는 다음 두 가지 덕목을 갖추고, 두 덕목 사이에서 균형을 유지해야 한다.

1. 객체는 협력적이어야 한다.
    객체는 다른 객체의 요청에 충실히 귀 기울이고 다른 객체에게 적극적으로 도움을 요청할 정도로 열려 있어야 한다. 모든 것을 처리하는 객체는 내부적인 복잡도에 의해 자멸하고 만다.

2. 객체는 자율적이어야 한다.
    '자율적' 이라는 단어의 뜻은 '자기 스스로의 원칙에 따라 어떤 일을 하거나 자기 스스로를 통제하여 절제하는 것'을 의미한다. 사물이 자신의 행동을 스스로 결정하고 책임진다면 그 사물을 자율적인 존재라고 한다.

회사에서 부서는 자율적인 존재로 구성된 협력 공동체다. 마케팅 팀은 마케팅을 기획하고 수행한다. 또한 마케팅에 필요한 자금을 집행하기 위해서는 재무 팀에 협력을 요청해야 한다. '마케팅' 업무에 관해서 마케팅 팀은 스스로 판단하고 행동한다. 마케팅 팀은 스스로 판단하여 '자금'에 대한 책임이 있는 재무팀에게 협력을 요청한다.

객체지향 설계의 묘미는 다른 객체와 조화롭게 협력할 수 있을 만큼 충분히 개방적인 동시에 협력에 참여하는 방법을 스스로 결정할 수 있을 만큼 충분히 자율적인 객체들의 공동체를 설계하는 데 있다.

#### 상태와 행동을 함께 지는 자율적인 객체

흔히 객체를 상태와 행동을 함께 지닌 실체라고 정의한다. 객체가 협력에 참여하기 위해 어떤 행동을 해야 한다면 그 행동을 하는데 필요한 상태도 함께 지니고 있어야 한다. 스스로 결정하는 자율적인 존재이기 위해서는 필요한 행동과 상태를 함께 지니고 있어야 한다.

객체의 자율성은 객체의 내부와 외부를 명확하게 구분하는 것에서 나온다. 객체의 사적인 부분은 객체 스스로 관리하고 외부에서 간섭할 수 없도록 차단해야 한다.

객체는 "상태와 행위를 하나의 단위로 묶는 자율적인 존재다." 따라서 외부와 내부가 엄밀히 구분되어야 한다. 객체의 외부에서는 접근이 허락된 수단을 통해서만 객체와 의사소통 해야한다. 객체는 다른 객체가 무엇을(what)을 수행하는지 알 수 있지만, 어떻게(how) 수행하는지에 대해서는 알 수 없다.

#### 협력과 메시지

"커피 주문"에서 요청과 응답은 객체지향 세계에서는 메시지다. 메시지는 객체지향 세계에서의 유일한 의사소통 수단이다. 메시지를 송신하는 객체를 송신자라 부르고, 메시지를 수신하는 객체를 수신자라고 부른다.

(프로세스간 메시지 전달이라는 .. 아키텍처가 생각이 난다.)

### 메서드와 자율성

객체가 수신된 메시지를 처리하는 방법을 **메서드**라고 부른다. (객체지향 프로그래밍의 특징은 런타임에 실행할 메서드를 선택할 수 있다는 점이다.)

메시지와 메서드의 분리를 분리하고, 객체가 메서드를 선택할 수 있는 것은 협력에 참여하는 객체들 간의 자율성을 증진시킨다. 바리스타가 자신만의 방법으로 자율적으로 커피를 제조할 수 있다.

**외부 요청이 무엇인지를 표현하는 메시지**와 요청을 **처리하기 위한 구체적인 방법인 메서드**를 분리하는 것은 객체의 자율 성을 높이는 핵심 메커니즘이다. 이는 캡슐화라는 개념과도 깊게 관련돼 있다.


## 객체지향의 본질

* 객체지향이란 프로그램을 상호작용하는 자율적인 객체들의 공동체로 바라보고 객체를 이용해 프로그램을 분할 하는 방법이다.

* 핵심은 적절한 책임을 수행하는 역할 간의 유연하고 견고한 협력 관계를 구축하는 것이다.

<br>
<br>

---
내 정리

* 객체지향 패러다임에서 어플리케이션은 책임을 수행할 수 있는 적절한 역할을 부여 받은 객체가 책임을 다하고, 다른 객체와 협력하여 구현된다. (역할, 책임, 협력 -> "커피 주문" 목표 수행)

* 객체는 협력적이고 자율적이어야 한다. 객체는 자율적이다. 스스로 판단하고, 행동한다. 자신이 책임지지 않는 부분은 다른 객체에 협력을 요청한다.

* 객체는 상태+행동.
    
    그런데 반드시 객체가 자율적이기 위해서 상태와 행동은 객체 내부와 외부가 분리되 있어야 한다.


* 메시지 - 객체의 유일한 의사소통 수단 / 메서드 - 메시지를 처리하는 방법
    
    메시지와 메서드의 분리 -> 객체들 간의 자율성 증진 (Java에서 메서드의 뜻과 좀 달라 보인다.) (public = 메시지)

    객체지향 언어에서 객체는 런타임에 메서드를 선택할 수 있다. (객체 내부의 상태에 따라 수행방법(how)이 선택될 수 있다는 뜻인 것 같다. DI 같은 것을 말하는 건 아닌 것 같고)

