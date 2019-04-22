---
layout: post
title: Vue 컴포넌트2
description: >
  사용자 정의 이벤트, 이벤트 버스, Slot, 동적 컴포넌트, keep-alive에 대해 학습합니다.
---

# 사용자 정의 이벤트, 이벤트 버스, Slot, 동적 컴포넌트, keep-alive

## 👉 사용자 정의 이벤트

경우에 따라서 양방향 바인딩이 필요할 수 있다.(*편리한  기능이긴 하지만 남용하지 말자.*)

이 때 두가지 방법을 사용할 수 있다.

- `v-on , $emit`
- `.sync`




#### v-on을 이용한 사용자 지정 이벤트

v-on을 이용해 사용자 지정 이벤트를 만들 수 있다.

이때 자식 컴포넌트는 `$emit`을 이용해 이벤트를 실행시킬 수 있다.

[예제 : https://codepen.io/devgaeng/pen/omvbBX](https://codepen.io/devgaeng/pen/omvbBX)



#### .sync

Vue.js 2.3 버전 부터 `.sync`라는 수식어를 지원

.sync 수식어는 일종의 `Syntax Sugar`

```js
<input :value="message" @update:value="value => message = value">
<!-- 위 코드는 다음과 같다 -->
    
<input :value.sync="message">
```

[예제 : https://codepen.io/devgaeng/pen/mvVOZr](https://codepen.io/devgaeng/pen/mvVOZr)



#### 컴포넌트의  v-model

v-model을 이용해 사용자 정의 입력을 만들 수 있다.

컴포넌트에  v-model을 사용하려면  valueprop과 input  이벤트를 사용해야 한다.

```js
<input v-bind:value="model"
	   v-on:input="model = $event.target.value"
>
<!-- 위 코드는 다음과 같다 -->
    
<input v-model="model">
```
[예제 : https://codepen.io/devgaeng/pen/YBzrWZ](https://https://codepen.io/devgaeng/pen/YBzrWZ)


## 👉 이벤트 버스 , Slot , 동적 컴포넌트(&keep-alive)

#### 부모 자식 관계가 아닌 컴포넌트의 통신

부모-자식 관계가 아닌 경우에도 통신이 필요할 때가 있다.

이 때, *비어있는  Vue 인스턴스*를 *이벤트 버스*로 이용해 해결할 수 있다.



[예제:https://codepen.io/devgaeng/pen/RvrvBN?editors=1010](https://codepen.io/devgaeng/pen/RvrvBN?editors=1010)

#### Slot

부모 컴포넌트는 자식 컴포넌트에게 `slot`을 이용해 템플릿을 전달할 수 있다.

이러한 방식을 *컨텐츠 배포*라고 한다.

slot 내부에 컨텐츠가 존재하고 부모컨텐츠가 비어있다면 slot 자체의 컨텐츠가

렌더링 되는데 이를 *대체 컨텐츠*라고 한다.

```html
<div id="app">
  <post>이 메시지가 'slot'에 전달</post>
</div>
<template id="post-tpl">
  <div>
    <h1>TITLE</h1>
    <p>
    	<slot></slot>
    </p>
  </div>
</template>
<script>
  Vue.component('post',{
    template : '#post-tpl'
  })

  new Vue({
    el : '#app'
  })
</script>
```



###### 이름을 가지는 slot

`slot` 엘리먼트는  name이라는 속성을 가질 수 있다.

name 속성을 이용하면 여러개의 `slot`을 사용할 수 있다.

```html
<div id="app">
  <post>
    <h1 slot="title">{{title}}</h1>
    <p slot="contents">{{contents}}</p>
  </post>
</div>
<template id="post-tpl">
  <div>
    <slot name="title">
      <!-- slot title here -->
    </slot>
    <slot name="contents">
      <!-- slot contents here -->
    </slot>
  </div>
</template>
<script>
    Vue.component('post',{
      template : '#post-tpl'
    })

    new Vue({
      el : '#app',
      data : {
        title : 'SLOT',
        contents : '부모 컴포넌트는 자식 컴포넌트에게 slot을 이용해 템플릿을 전달할 수 있다.'
      }
    })
</script>
```



###### 범위를 가지는 slot

`v-for`를 사용해 범위를 지닌 slot의 경우 template 엘리먼트와 scope 속성을 통해 처리할 수 있다.

```html
<template scope="props">
```

여기서  `scope`는 자식 컴포넌트의 slot으로 부터 전달된 값을 저장하는 임시 변수의 명을 지정한다.
(꼭 props일 필요는 없다.)

[예제 : https://codepen.io/devgaeng/pen/pGgGMV](https://codepen.io/devgaeng/pen/pGgGMV)





#### 동적 컴포넌트

- component 엘리먼트를 사용해 여러 컴포넌트를 동적으로 전환할 수 있다. (ex. tab menu)
- 동적 컴포넌트 사용중 컴포넌트의 상태를 유지하고 싶다면 keep-alive 엘리먼트를 사용해 해결할 수 있다.

[예제 : https://codepen.io/devgaeng/pen/daMbVL](https://codepen.io/devgaeng/pen/daMbVL)



#### v-once

- 정적 컨텐츠를 렌더링 할 경우 여러번 캐시될 필요가 없기 때문에, 이때 `v-once`를 사용한다.
- `v-once`디렉티브를 사용하여 업데이트 되지 않는 이로히성 보간을 수행할 수 있지만,같은 노드의 바인딩에도 영향을 미친다는 점을 유의해야 한다.


 *Thanks to*

[도서 Vue.js 이정도는 알아야지](http://www.yes24.com/Product/Goods/56894866)  