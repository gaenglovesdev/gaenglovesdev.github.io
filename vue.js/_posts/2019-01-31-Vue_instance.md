---
layout: post
title: Vue 인스턴스
description: >
  vue 인스턴스에 대해서 학습합니다.
---

**단일 파일 컴포넌트를 학습하기 전까지는 CDN 혹은 JSFIDDLE , CODEPEN로 코드를 작성하여 포스팅합니다.**

VUE CDN  : `<script src="https://cdn.jsdelivr.net/npm/vue"></script>`



## 👉 인스턴스 생성

`Vue 인스턴스`의 생성은 Vue앱을 시작하기 위해 필수적이며,
앱의 시작은 곧 Vue 인스턴스를 만드는것부터 시작한다. 간단한 템플릿 렌더링부터 데이터 바인딩, 
컴포넌트 등 많은 동작을 한다.
Vue 인스턴스를 생성할 때, 여러 옵션들을 담은 객체를 전달해야한다.
(ex. element , data , lifecycle)


```html
<!--html-->
<div id="app">
  {% raw %}{{ message }}{% endraw %}
</div>
```

```js
//JS
const app = new Vue({
  el: '#app', // Vue 인스턴스가 작동할 엘리먼트를 지정
  data: {
    message: 'My friend Vue.js'
  }
})
```

## 👉 데이터와 메서드

#### 데이터(Data)
Vue 인스턴스의 데이터는 화면에 데이터를 출력하기 위해 정의 되어야 한다.
String,Number,Array,Object 등등 어떤 타입으로도 정의 가능하다.
다음은 사용법이다.

```js
new Vue({
  el : '#app',
  data : {
    message : 'Hello Vue , Hello Gaeng!', //String
    price : 99000, // Number
    members : ['CHO','GAENG'], // Array
    userInfo : { // Object
      name : 'gaeng',
      gender : 'man'
    }
  }
})
```

#### 메서드(Methods)

위 `data` 속성에 정의된 데이터는 View와 상호작용하는데 쓰이거나 Vue 인스턴스 내부에서 로직을 연산할 때
사용될 수 있다. 다음은 메서드를 정의하는법과 사용하는 법이다.

```html
<div id="app">
  <button @click="sayHello()">Say Hello!</button>
</div>
```

```js
new Vue({
  el : '#app',
  data : {
    message : 'Hello Vue , Hello Gaeng!', //String
  },
  methods : {
    sayHello(){
      alert(this.message)
    }
  }
})
```

html 코드 내부의 버튼에 `이벤트 바인딩`이라는 템플릿 문법중하나인 클릭 이벤트가 연결 되어있고,
클릭 이벤트가 이루어 질 경우 해당 구문안의 표현식이 호출되는 문법이다.
해당 버튼을 클릭하게 되면 sayHello() 메서드가 실행되게 된다.


## 👉 계산된 속성(Computed)

템플릿 내에서 사용하는 표현식은 잘못 사용할 경우 가독성이 떨어져 유지보수가 어려워 질 수 있다.
다음은 예시이다.

```html
<div id="app">
  <!--문자열-->
  <p>{{ message }}</p>
  <!--문자열 역순-->
  <p>{{ message.split('').reverse().join('') }}</p>
</div>
```

```js
new Vue({
  el : '#app',
  data : {
    message : 'Hello Vue , Hello Gaeng!' 
  }
})
```

위 같은 코드들이 많아질수록 유지보수가 어려워질 것이다.
이럴 경우 method에 정의 해놓고 호출하는것도 좋은 방법이지만,
Vue 인스턴스의 `계산된 속성(computed)`를 사용하면 종속성이 있는 데이터에 따라 캐시가 된다. 
변경에 잦은 데이터에 대해서는 더 좋은 성능을 기대할 수 있다.

```html
<div id="app">
  <!--문자열-->
  <p>{{ message }}</p>
  <!--문자열 역순-->
  <p>{{ reverseMessage }}</p>
</div>
```

```js
new Vue({
  el : '#app',
  data : {
    message : 'Hello Vue , Hello Gaeng!'
  },
  computed : {
    reverseMessage(){
      return this.message.split('').reverse().join('')
    }
  }
})
```

## 👉 감시된 속성(Computed)

감시도니 속성은 Vue 인스턴스의 데이터가 변경되는 시점을 감시해 메서드를 호출하는 기능이다.
라이프 사이클이 Vue 인스턴스의 이벤트를 후킹하는 것이라면, 감시된 속성은 Vue 인스턴스의 데이터의 변경을 후킹하는것이다.

```html
<div id="app">
  <input v-model="search" type="text">
  <!--문자열-->
  <p>{{ search }}</p>
</div>
```

```js
new Vue({
  el : '#app',
  data : {
    search : ''
  },
  watch : {
    search(value){
      this.$http.get('/search?value='+value)
        .then(response => {
          /* ... */
        })
    }
  }
})
```

*Thanks to*

[도서 Vue.js 이정도는 알아야지](http://www.yes24.com/Product/Goods/56894866)  
[Jeong Woo Ahn - Vue.js 2.0 라이프사이클 이해하기](https://medium.com/witinweb/vue-js-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-7780cdd97dd4)  

