---
layout: post
title: Vue 컴포넌트1
description: >
  Vue 로컬, 글로벌 컴포넌트에 대해서 학습합니다.
---
# 글로벌 컴포넌트, 로컬 컴포넌트

## 👉 글로벌 컴포넌트

- 생성
```js
  Vue.component('date',{
    template : '<div>{{now}}</div>',
    data : function(){
      return {
        now : new Date()
      }
    }
  })
```
- `Vue.component`는 컴포넌트를 전역으로 등록하는 메서드이다.
- `data`를 정의할때는 `반드시` 함수로 정의해야 한다.

## 👉 로컬 컴포넌트

- 컴포넌트를 Vue 인스턴스 혹은 컴포넌트의 옵션으로 등록해 컴포넌트 내부에서만
사용하도록 지정할 수 있다.

- 제한사항
	- ul,ol,table,select 같은 일부 엘리먼트 내부에서는 컴포넌트를 사용할 수 없다.
    - `is` 옵션을 사용해 정상적으로 렌더링 할 수 있다.

    ```html
		X
		<table>
      <hello-world></hello-world>
      <hello-world></hello-world>
      <hello-world></hello-world>
    </table>
    ```
    ```html
		O
		<table>
      <tr is="hello-world"></tr>
      <tr is="hello-world"></tr>
      <tr is="hello-world"></tr>
    </table>
    ```
- 템플릿 분리
 - 템플릿을 분리해 정의할 수 있다.

 ```html
  <template id="hello-world">
      <tr>
        <td>VUE</td>
        <td>REACT</td>
        <td>ANGULAR</td>
      </tr>
  </template>
```

or

```html
<script type="text/x-template" id="hello-world">
  <tr>
      <td>VUE</td>
      <td>REACT</td>
      <td>ANGULAR</td>
  </tr>
</script>
```

```js
  const HelloWorld = {
  	template : '#hello-world', //해당 template id
      data : function(){         //함수로 정의
        return {
          hello : 'world'
        }
      },
  }
  new Vue({
     el : '#app',
       components : {
       'hello-world' : HelloWorld
     }
  })
```
- 데이터 전달 (Props)
 - 모든 컴포넌트는 템플릿에서 부모 컴포넌트의 데이터를 참조할 수 없다.
 - 부모 컴포넌트 데이터를 참조하기 위해선 `Props` 옵션을 사용해 전달 할 수 있다.
 - 네이밍 규칙 : HTML은 대소문자를 구분하지 않으므로  kebab-case를 사용 스크립트에서는 camelCase를 이용해줍니다. (props 옵션에서는 자동변환되어 사용)

```html
<div id="app">
    <some-component simple-message="Props"></some-component>  
</div>
```

```js
const someComponent = {
      props : ['simpleMessage'],
      templete : '#some-component'
}
```

 - 동적 데이터를 전달하고 싶으면 v-bind를 이용해 전달
 - 데이터 전달은 부모 > 자식으로 단방향으로 흐른다. 따라서 부모가 전달한  Props를 수정할 수 없다.
 변경이 필요하다면
   - Props의 초기값을 컴포넌트 로컬 데이터로 정의
   - Props 로부터 계산된 속성을 정의
 - Prop 검증
 	Props로 데이터를 전달 받을 때 데이터 타입을 강제할 수 있다.
    
예제

[SIMPLE TODO - https://codepen.io/devgaeng/pen/BvMOzB?editors=1010](https://codepen.io/devgaeng/pen/BvMOzB?editors=1010)

[CITY LIST - https://codepen.io/devgaeng/pen/EGMMJg](https://codepen.io/devgaeng/pen/EGMMJg)

[EACH COUNTER - https://codepen.io/devgaeng/pen/LMoPww](https://codepen.io/devgaeng/pen/LMoPww)


 *Thanks to*

[도서 Vue.js 이정도는 알아야지](http://www.yes24.com/Product/Goods/56894866)  