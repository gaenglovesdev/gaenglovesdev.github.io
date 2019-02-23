---
layout: post
title: 유용한 Vue.js 플러그인
description: >
canonical_url:
---

# 유용한 Vue.js 플러그인

## Vue-axios

*Axios*는 동적으로 데이터를 불러오기 위한 네트워크 라이브러리이다.  
Vue.js에서는 *vue-resource*와  *axios*가 대표적인 네트워크 라이브러리인데
커뮤니티가 좀 더 활발하고 , 업데이트가 빠르기 때문에 *axios*로 사용한다.



#### 설치  

```
//npm
npm install --save axios vue-axios

//yarn
yarn add -S axios vue-axios
```

#### 예제

[Axios 사용법 - https://www.npmjs.com/package/axios](https://www.npmjs.com/package/axios)

```js
// src/main.js
import Vue from 'vue'
import App from './app'
import axios from 'vue'
import VueAxios from 'vue-axios'

Vue.use(VueAxios,axios)

new Vue({
    el : '#app',
    template : '<App/>',
    components : { App }
})
```

```vue
<!-- src/App.vue -->
<template>
  <div id="app">
    <button @click="fetchPosts">불러오기</button>
    <div v-for="post in posts">
      <h1>{{ post.title }}</h1>
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      posts: []
    }
  },
  methods: {
    fetchPosts () {
      this.axios.get('https://jsonplaceholder.typicode.com/posts')
        .then((response) => {
          this.posts = response.data
        })
    }
  }
}
</script>

```





## vue-router

SPA 프로젝트에서 먼저 처리해야 할 것이 라우팅인데 , 서버에서 라우팅은 URI에 따라 해당하는  

정적 파일을 내려주는 방식이다. SPA를 구현할 경우 화면 컨텐츠 출력을 위해 ajax를 사용하고,  

*[hashbang](https://m.blog.naver.com/PostView.nhn?blogId=writer0713&logNo=220179565314&proxyReferer=https%3A%2F%2Fwww.google.com%2F)* 혹은 *[PushState](https://www.zerocho.com/category/HTML&DOM/post/599d2fb635814200189fe1a7)*를 사용해야 한다.

단순한 라우팅을 직접 구현할 수도 있지만, 전용 라이브러리를 사용하는 것이 좋다.  
공식문서에서는 *vue-router* 라이브러리를 추천하고 있다.



## vuex

*vuex*는 상태 관리 패턴 플러그인이다. vue app의 모든 컴포넌트에 대한 글로벌 저장소 역할을 하면서 사이드 이펙트 없이 상태를 변경할 수 있다. 여러 컴포넌트에서 하나의 데이터를 공유할 때 혹은 수평적인 컴포넌트 간의 데이터 공유가 필요할 때 vuex를 사용하게 되는데 , 이전에는 같은 문제를 해결하기 위해 *Event bus*를 구현해서 문제를 해결했으나, App의 규모가 커질때에는 event bus보다는 vuex를 통해 관리하는 것이 좀 더 효율적이다.  상태관리의 여러 문제점을 해결하기 위해 데이터 통신을 한 곳에서 중앙 집중식으로 관리한다.

![vuex-diagram](/assets/images/vue/vuex-diagram.png)

#### State

state에 정의된 속성들은 컴포넌트 간의 공유할 data 속성을 의미한다.

#### Mutations

Mutations 이란 Vuex 의 데이터, 즉 state 값을 변경하는 로직들을 의미한다.
State에 있는 데이터를 변경할 때, 직접 state에 접근하여 변경하였지만, 이는 안티패턴으로써,

예를들어 여러 컴포넌트에서 같은 state값을 동시에 제어하게 되면, state값이 어느 컴포넌트에서 호출해서 변경된건지 추적하기가 어렵기 때문이다. 

*commit()* 메서드를 이용해 값을 넘긴다.

#### Actions

Mutations의 역할 자체가 State 관리에 주안점을 두고 있다. 상태관리 자체가 한 데이터에 대해 여러 개의 컴포넌트가 관여하는 것을 효율적으로 관리하기가 위함인데 Mutations에 비동기 처리 로직들이 포함되면 같은 값에 대해 여러 개의 컴포넌트에서 변경을 요청했을때,그 변경 순서 파악이 어렵기 때문이다.

이런 문제를 방지하기 위하여 비동기 로직은 *actions*에 동기 로직은 *Mutations*에 나눠 구현한다.

(전체 구조도에서의 dispatch의 동작)
![vuex-diagram](/assets/images/vue/vuex-actions.png)

```js
// App.vue
methods: {
  // 기존 state에 직접 접근
  addCounter() {
    this.$store.state.counter++;
  }
  // Mutations 를 이용할 때
  addCounter() {
    //this.$store.state.counter++;
    this.$store.commit('addCounter');
  }
  // Actions 를 이용할 때
  addCounter() {
    this.$store.dispatch('addCounter');
  }
},
```

```js
//store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
	counter : 0
  },
  mutations: {
	addCounter: function (state, payload) { // 특정한 값을 넘기고 싶을땐 두번째 인자를 추가
        								   // 통용적으로 payload라는 이름을 많이 쓴다.
        state.counter = payload.value;
    }
  },
  actions: {
	addCounter: function (context) {
        return context.commit('addCounter');
    }
  }
})

```




*Thanks to*

[참고 : 도서 Vue.js 이정도는 알아야지](http://www.yes24.com/Product/Goods/56894866)  
[참고 : 김정환 블로그 - Vue Router 알아보기](http://blog.jeonghwan.net/2018/04/07/vue-router.html)  
[참고 : 캡틴판교 - vuex 시작하기1](https://joshua1988.github.io/web-development/vuejs/vuex-start/)  
[참고 : 캡틴판교 - vuex 시작하기2](https://joshua1988.github.io/web-development/vuejs/vuex-getters-mutations/)  
[참고 : 캡틴판교 - vuex 시작하기3](https://joshua1988.github.io/web-development/vuejs/vuex-actions-modules/)  

