---
layout: post
title: Vue 인스턴스
description: >
  A page showing how regular markdown content is styled in Hydejack.
image: /assets/img/blog/example-content-ii.jpg
canonical_url: https://pages-themes.github.io/architect/
---

*단일 파일 컴포넌트를 학습하기 전까지는 CDN 혹은 JSFIDDLE , CODEPEN로 코드를 작성하여 포스팅합니다.*

VUE CDN  : `<script src="https://cdn.jsdelivr.net/npm/vue"></script>`



## 인스턴스 생성

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

