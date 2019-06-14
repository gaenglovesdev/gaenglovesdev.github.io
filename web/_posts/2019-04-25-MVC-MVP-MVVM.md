---
layout: post
title: "MVC, MVP, MVVM"
description: >
  MVC, MVP, MVVM 패턴을 알아보자
category: Web
---
# 소프트웨어 아키텍쳐 패턴 - MVC,MVP,MVVM (Architecture pattern)

## ☝️ 아키텍쳐 패턴이란?

- 소프트웨어 요소와 이들 요소의 외부 속성, 그리고 이들 사이의 관계를 구성하는 시스템 구조이다.(시스템의 전반적인 구조)
- 시스템의 컴포넌트와 이들 사이의 관계, 그리고 이들의 설계 및 변경에 대한 원리와 가이드라인을 정의한 구조이다.
- 소프트웨어 디자인 패턴과는 유사하지만, 좀 더 큰 개념을 지칭


## 👉 MVC, MVP, MVVM


### MVC(Model + View + Controller)

![MVC 패턴](/assets/images/pattern/mvc.png)

#### 구성

> MODEL : 프로그램에서 사용되는 실제 데이터 및 데이터 조작 로직을 처리하는 부분

Model은 프로그램에서 사용되는 실제 데이터이며 불러오거나 업데이트 하는 로직이 추가 되어 있다.

> VIEW : 사용자에게 제공되어 보여지는 UI 부분

View는 실제 사용자가 눈으로 보고 있는 화면이다.

> CONTROLLER : 사용자의 입력을 받고 처리하는 부분

Controller는 사용자의 입력을 받은 다음 해당 작업을 처리 하는 부분이다.

#### 동작

1. controller로 사용자의 입력이 들어온다.
2. controller는 Model의 데이터 업데이트를 한다.
3. model은 해당 데이터를 보여줄 View에 데이터를 출력한다.

#### 단점

View와 Model이 서로 의존적이라는 부분이 단점이다.(의존성은 최대한 줄여야한다.)

### MVP(Model + View + Controller)

![MVP 패턴](/assets/images/pattern/mvp.png)

#### 구성

Model 과 View는 **MVC**와 같다.

> PRESENTER : View에서 요청한 정보를 Model로 부터 가공해서 View로 전달하는 부분

Model과 View는 MVC와 동일하지만 사용자 입력을 View에서 받는다.
그리고 Model과 View는 각각 Presenter와 상호 동작을 하게 된다.
MVC의 단점이였던 `view`와 `model`의 의존성이 없어지게 된다.

#### 동작

1. View로 사용자의 입력이 온다.
2. View는 Presenter에 작업 요청을 한다.
3. Presenter에서 필요한 데이터를 Model에 요청한다.
4. Model은 Presenter에 필요한 데이터를 응답한다.
5. Presenter는 View에 데이터를 응답한다.
6. View는 Presenter로부터 받은 데이터로 화면에 출력한다.

#### 단점

view와 model의 의존성이 없는 대신 View와 presenter가 1:1 강한 의존성을 갖게 된다.

### MVVM(Model + View + Controller)

![MVVM 패턴](/assets/images/pattern/mvvm.png)

MVVM은 Controller,Presenter 대신 ViewModel이 존재한다.

>VIEWMODEL : View를 표현하기 위해 만들어진 View를 위한 Model

MVVM은 두가지 디자인 패턴 Command패턴과 Data Binding을 사용하는데,
이 두가지 패턴으로 인해 View와 ViewModel은 의존성이 사라지게 된다.
View에서 입력이 들어오면 Command 패턴을 통해 ViewModel에 명령을 내리게 되고
Data Binding으로 인해 ViewModel의 값이 변화하면 바로 View의 정보가 새로 갱신되게 된다.

#### 동작

1. View에 입력이 들어오면 Command 패턴으로 ViewModel에 알린다.
2. ViewModel은 필요한 데이터를 Model에 요청한다.
3. Model은 ViewModel에 필요한 데이터를 응답한다.
4. ViewModel은 응답 받은 데이터를 가공해서 저장한다.
5. View는 ViewModel과의 Data Binding으로 인해 자동으로 갱신된다.

*Thanks to*

[참고 : pds12 - 소프트웨어아키텍처 소프트웨어아키텍처 개념의 이해](http://pds12.egloos.com/pds/200901/14/88/a0105788_496df5c87a456.pdf)

[참고 : 마기의 개발 블로그 - MVC, MVP, MVVM 비교](https://magi82.github.io/android-mvc-mvp-mvvm/)