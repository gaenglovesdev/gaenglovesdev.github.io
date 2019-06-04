---
layout: post
title: "FLUX pattern"
description: >
  FLUX 패턴을 알아보자
category: Web Front-end
---
# FLUX 패턴(Flux pattern)

## ☝️ Flux 패턴이란?

- Flux 패턴은 MVC의 문제를 해결할 목적으로 Facebook에서 고안한 어플리케이션 아키텍처 패턴이다.
- Dispatcher, Store, View 세 부분으로 나뉜다.
- 단방향 데이터 흐름의 특징을 가진다.

## 👎 MVC패턴의 단점
![일반적인 MVC 패턴](/assets/images/pattern/mvc-normal.png)
<div style="margin:0 auto;font-size:12px;text-align:center;">[일반적인 MVC 패턴]</div>

[MVC패턴](/web/web%20front-end/2019-04-25-MVC-MVP-MVVM/)의 의도는 각자의 역할, 맡은바에 집중을 할 수 있게
개발을 하여 유지보수와 확장성을 위해 만들어진 패턴이다. 하지만 Model과 View가 추가될수록 프로젝트는 복잡해지고
유지보수를 힘들게 한다.

![복잡해진 MVC 패턴](/assets/images/pattern/mvc-complexity.png)
<div style="margin:0 auto;font-size:12px;text-align:center;">[복잡해진 MVC 패턴]</div>

실제 페이스북에서는 어플리케이션의 규모가 커지고, 구조가 복잡해져 기능추가 때마다 크고 작은 문제가 생겼고,
이에 페이스북 개발팀은 Flux패턴을 고안하게 된다.

## 👉 Flux패턴의 특징

가장 큰 특징으로 **단방향 데이터 흐름**들 수 있고 데이터는 항상
***Dispatcher -> Store -> View*** 순으로 흐르고 다시 ***View -> Action -> Dispatcher***로 흐른다.

![Flux 패턴](/assets/images/pattern/flux_simple.png)


#### 디스패처 (Dispatcher)

디스패처는 어플리케이션의 중앙 허브로써 모든 데이터 흐름을 관리하는 역할을 한다.
스토어의 콜백을 등록하는데 쓰이고 디스패처로 전달된 액션을 스토어에 전달하는 역할을 한다.


#### 스토어 (Store)

스토어는 어플리케이션의 상태를 저장하고 로직을 포함한다. MVC의 모델과 비슷하지만 많은 객체의 상태를
관리할 수 있다. 디스패처에 콜백함수를 등록하여 메시지를 수신하고, 스토어가 변경되면 뷰에 변경내용을 반영한다.

#### 뷰 (View)

MVC의 뷰와는 달리 화면을 표시하는 것은 물론 컨트롤러의 성격도 가지고 있다.
최상위의 뷰는 스토어에서 데이터를 받아 이를 자식뷰로 배분하는 역할을 해 Controller-view라고도 부른다.

#### 액션 (Action) 
디스패처에서 콜백 함수가 실행할 때 데이터묶음을 인수로 전달하는데 이 객체를 Action이라 하고
대체로 액션은 액션생성자(Action creator)에서 만들어진다.

![Flux 패턴](/assets/images/pattern/flux_with_action.png)



*Thanks to*

[참고 : Flux](https://haruair.github.io/flux/docs/overview.html)

[참고 : 코드쓰는사람 - Flux와 Redux](https://taegon.kim/archives/5288)