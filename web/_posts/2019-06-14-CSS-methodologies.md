---
layout: post
title: "CSS 방법론"
description: >
  BEM,OOCSS를 알아보자
category: Web
---

# CSS 방법론(CSS methodologies)

웹의 발전으로 인해 CSS의 역할도 커져갔고 복잡한 설계의 필요성 조차 필요없었던
CSS에도 다양한 방법론이 생기기 시작했다. 그리고 방법론들은 모두 같은 지향점을 갖는다.

- 코드의 재사용성
- 유지보수의 용이성
- 확장 가능성
- 클래스 네임만으로 해당 엘리먼트의 역할 예측

대표적인 방법론인 **BEM**와 **OOCSS**에 대해서 알아보자.


## 🧐 BEM(Block,Element,Modifier)은?

--- 

- Block, Element, Modifier의 약자이다.
- OOP와 유사하다.
- ID는 사용할 수 없고, class명만 사용 가능하다.
- ex) block__element--modifier

### 작명규칙

#### BLOCK

문단 전체에 적용된 element 또는 element를 담고 있는 컨테이너를 말한다.

```html
<header class="header">
    <div class="something"></div>
    <div class="something"></div>
</header>
```

#### Element

- element는 block 안에서 특정 기능을 수행하는 컴포넌트이다. element는 언더스코어( _ ) 두개로 block과 연결하여 표기한다.
- block과 element의 이름이 길 경우 하이픈( - )으로 연결한다.

```css
.header__logo { ... };
.header__nav { ... };
.header__menu { ... };

.header__something-menu { ... };
.header__something-btn { ... };
```

#### Modifier

- Modifier은 block 또는 element의 속성이다.
- 이 속성은 element의 외관이나 상태를 변화시킨다.
- element와 하이픈( - ) 두개로 연결하여 표기한다.

```css
.nav__menu { ... };
.nav__menu--secondary { ... };
```

BEM은 클래스명만으로도 구조를 유추할 수 있고, 간단한 작명규칙이다.
확실한 약속이 있기 때문에 협업간에도 유용하게 쓰일 수 있다.
*단점*은 클래스명이 꽤 길어지고, 괴이해지기 때문에 처음 접한사람은
거부감이 들 수 있다.


![BEM with ryan](/assets/images/css_methodology/bem_with_ryan.png)

<div style="margin:0 auto;font-size:12px;text-align:center;">BEM with ryan of kakao</div>

## 🧐 OOCSS(Object Oriedted CSS)는?

---

- Nicole Sullivan에 의해 개발된 프레임워크
- CSS를 모듈 방식으로 코딩하여 중복을 최소화하는 기법
- 코드의 재사용성 증가
- 자손선택자의 사용을 지양한다.
- 구조와 외양을 분리


```css
.btn {
  ...
}
.popup {
  ...
}

.red{
  background-color:red;
  color:#fff;
}
```

<div style="margin:0 auto;font-size:12px;text-align:center;">구조와 외양의 분리 예제</div>

### 작명 규칙

- 간결함 : 짧게
- 명료함 : 스타일과 작동 방식이 고스란히 드러나게
- 분명한 말뜻 : 어떻게 생겼는지 보다, 어떤 모듈인지

### 예제

```css
.facebookbtn{
  width:100px;
  height:50px;
  color:#fff;
  border-radius:4px;
  background-color:#000;
}

.instabtn{
  width:100px;
  height:50px;
  color:#fff;
  border-radius:4px;
  background-color:#777;
}
```

<div style="margin:0 auto;font-size:12px;text-align:center;">중복스타일 제거 전</div><br>


```css
.btn{
  width:100px;
  height:50px;
  color:#fff;
  border-radius:4px;
}
.facebookbtn{
  background-color:#000;
}
.instabtn{
  background-color:#777;
}
```

<div style="margin:0 auto;font-size:12px;text-align:center;">중복스타일 제거 후</div><br>

## BEM? OOCSS? or OTHERS?

본문에 언급하지 않은 다른 멋진 방법론들과 BEM,OOCSS중에 무엇을 선택해야 할지는
규모와 상황에 따라 달라지겠지만 필자의 경우 BEM과 OOCSS 를 **혼용** 하고 있다.
거기에 전처리기를 사용한다면 좀 더 강력한 힘을 낼 수 있다.

*Thanks to*

[참고 : 재희 jaiyah - BEM(Block Element Modifier) 방법론](https://webclub.tistory.com/263)

[참고 : Jeongmin - [CSS방법론] SMACSS, BEM, OOCSS](https://wit.nts-corp.com/2015/04/16/3538)