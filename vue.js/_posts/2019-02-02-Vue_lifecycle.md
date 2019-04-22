---
layout: post
title: Vue 라이프사이클
description: >
  vue 라이프사이클 대해서 학습합니다.
---

# 라이프사이클(lifecycle)

`라이프사이클`이란 Vue 인스턴스의 생성부터 파괴까지 이렬ㄴ의 과정을 의미한다.
대략적으로 **생성 > 마운트 > 업데이트 > 파괴**의 과정을 거치고, 대부분의 인스턴스는 업데이트 사이클에 
머물러 있다. 사용자는 vue 인스턴스의 옵션을 통해 라이프사이클 훅을 정의할 수 있다.

![vue 라이프사이클](/assets/images/vue/lifecycle.png)

```js
new Vue({
  el : '#app',
  created(){
    console.log('Vue 인스턴스가 created 될 때 실행된다.')
  },
  mounted(){
    console.log('Vue 인스턴스가 mounted 될 때 실행된다.')
  },
  updated(){
    console.log('Vue 인스턴스가 updated 될 때 실행된다.')
  },
  destroyed(){
    console.log('Vue 인스턴스가 destroyed 될 때 실행된다.')
  }
})
```

## 👉 생성(creation)

라이프사이클 중에서 가장 처음 실행된다. 컴포넌트가 돔에 추가 되기 전이고,
**서버사이드 렌더링**에서도 지원되는 훅이다. 클라이언트와 서버에서 처리해야할 일이 있다면
이 단계에서 진행한다.

- beforeCreate : 모든 훅 중에 가장 먼저 실행되는 훅이다. 아직 data와 events(vm.$on, vm.$once, vm.$off, vm.$emit)가 세팅되지 않은 시점이다 접근시 에러가 난다.
- created :created 훅에서는 data와 events가 활성화되어 접근할 수 있다. 여전히 템플릿과 가상돔은 마운트 및 렌더링되지 않은 상태이다.

## 👉 마운트 / DOM 삽입단계 (Mounting)

Mounting 단계는 초기 렌더링 직전에 컴포넌트에 직접 접근할 수 있다.
초기 랜더링 직전에 돔을 변경하고자 한다면 이 단계를 활용할 수 있다.
그러나 컴포넌트 초기에 세팅되어야할 데이터 패치는 created 단계를 사용하는것이 낫다.

- beforeMount : 템플릿과 렌더 함수들이 컴파일 된 후, 첫 렌더링이 일어나기 직전에 실행된다.
- mounted : 컴포넌트, 템플릿, 렌더링 된 DOM에 접근할 수 있다. 모든 하위 컴포넌트가 마운트된 상태를 보장하지는 않는다.
  - 중요한점은 부모-자식간의 컴포넌트에서의 mounted 훅의 순서는 자식 -> 부모순으로 실행된다 (created의 반대)

## 👉 업데이트 / Diff 및 재렌더링 단계 (Updating)

컴포넌트가 어떠한 이유로 재렌더링 시 실행된다/ 디버깅이나 프로파일링 등을 위해 재렌더링 시점을 알고 싶을때
사용을 추천한다.

- beforeUpdate : 컴포넌트의 데이터가 변하여 업데이트 사이클이 시작될때 실행된다. DOM 패치 직전에 실행된다.
- updated : 컴포넌트의 데이터가 변하여 재 렌더링이 일어난 후에 실행된다. 그러나 여기서 상태를 변경하면 무한루프에 빠질 수 있다. 모든 자식 컴포넌트의 재 렌더링 상태를 보장하지는 않는다.

## 👉 파괴 / 해체 단계 (Destruction)

- beforeDestroy : 해체(vue 인스턴스 제거) 직전전에 실행된다. 이벤트 리스너를 제거하거나 reactive subscription을 제거하고자 한다면 이 훅이 제격이다.
- destroyed : 해체(vue 인스턴스 제거) 후에 실행된다. Vue 인스턴스의 모든 디렉티브가 바인딩 해제 되고 모든 이벤트 리스너가 제거되며 모든 하위 Vue 인스턴스도 삭제된다.