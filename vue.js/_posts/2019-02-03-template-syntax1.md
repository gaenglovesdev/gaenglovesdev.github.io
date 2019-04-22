---
layout: post
title: Vue 템플릿 문법1
description: >
  데이터바인딩,조건문,반복문에 대해서 학습합니다.
---

# 데이터 바인딩,조건문,반복문

Vue는 `Template` 블럭의 내용을 파싱하여 view에 뿌려준다. 템플릿 문법은 `template` 블럭에서 사용하는 문법을
지칭하고, 이 문법을 사용하면 만들어진 데이터를 이용해 `template` 블럭 내에서 DOM 조작이 가능하다.
템플릿 문법은 주로 `Directive`로 이루어져 있다.

`<div v-if="isShow">Hello, gaeng!</div>`


## 👉 데이터 바인딩

데이터 바인딩이란 템플릿과 Vue 인스턴스의 데이터를 연결하는 것을 의미한다.
방법은 다양하지만 대표적인 4가지 방법은 아래와 같다.

- Mustache
- v-text
- v-html
- v-bind

#### Mustache

`{% raw %}{{ expression }}{% endraw %}`

가장 쉬운 데이터 바인딩 문법으로써, 중괄호의 모양이 콧수염(expression)을 연상시키기 때문에 이름 붙여졌다.
데이터 값이 변경된다면 바인딩된 View도 변경된 값으로 다시 템플릿을 렌더링한다.


#### v-text

Mustache와 거의 동일하게 작동한다. 중괄호 대신 디렉티브를 이용해 데이터를 바인딩한다.

```html
<div id="app">
  <p v-text="greeting"></p>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    greeting: '안녕하세요!'
  }
})
```

RESULT:

```
안녕하세요!
```

#### v-html

`v-html`은 `v-text`와 달리 HTML 문자열을 그대로 바인딩한다.

```html
<div id="app">
  <p v-text="greeting"></p>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    greeting: '안녕<br>하세요!'
  }
})
```

RESULT:

```
안녕
하세요
```
#### v-bind

`v-bind`는 View의 텍스트를 렌더링하는 문법이 아닌 태그의 속성에 데이터를 바인딩하는 문법이다.
`v-bind`은 `:`로 바꿔서 줄여 쓸 수 있다.

`v-bind:href="something"` 👉 `:href="something"`

```html
<div id="app">
  <a v-bind:href="github">github</p>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    github: 'https://github.com/gaenglovedev'
  }
})
```


## 👉 조건문

템플릿에서 DOM 엘리먼트를 조건에 따라 보여 주거나 보여 주고 싶지 않은 경우가 있을 수 있다.
이 경우 템플릿 문법의 조건문을 사용하면 쉽게 해결할 수 있다.

#### v-if

`v-if`를 사용해 조건에 따라 템플릿을 보여 줄 수 있다.
조건이 참일 경우 해당 템플릿을 보여준다.

```html
<div id="app">
  <div v-if="isShow">SHOW</div>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    isShow: true
  }
})
```

#### v-else , v-else-if

두 문법은 `v-if`의 조건에 맞지 않는 경우에 보여질 템플릿을 정의 할 수 있다.

```html
<div id="app">
  <div v-if="name === 'gaeng'">GAENG</div>
  <div v-else-if="name === 'cho'">CHO</div>
  <div v-else>GEUN</div>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    name: 'gaeng'
  }
})
```

#### template if

`v-if`는 디렉티브 이기 때문에 한 가지 엘리먼트 밖에 적용할 수 없다. 여러 엘리먼트를 처리해야 할 경우,
`template` 엘리먼트를 사용해 해결할 수 있다. `template`엘리먼트의 경우 가상의 엘리먼트이기 때문에
실제로는 자식 엘리먼트만 렌더링 된다.

```html
<div id="app">
  <template v-if="soldOut">
      <h1>SOLD OUT</h1>
      <p>해당 제품은 품절입니다.</p>
  </template>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    soldOut: true
  }
})
```

#### v-show

`v-show`는 `v-if`와 비슷한 동작을 한다. 조건이 true일 경우 렌더링하고 false일 경우에는 렌더링 하지 않는다.


#### v-if vs v-show

차이점을 알아보자.

|                     v-if                     |              v-show              |
|:--------------------------------------------:|:--------------------------------:|
| 초기 조건이 false일 경우 렌더링 하지 않는다. |         항상 렌더링 된다.        |
|  조건이 false가 될 경우 엘리먼트가 삭제된다. |   CSS display 속성을 토글한다.   |
|           template 구문을 지원한다.          | template 구문을 지원하지 않는다. |
|           v-else를 사용 할 수 있다.          |     v-else를 사용 할 수 없다.    |


## 👉 반복문

Vue.js에서 엘리먼트를 반복해 출력할 수 있는 문법을 알아보자.

#### 범위 v-for

`v-for` 디렉티브는 반복적인 엘리먼트를 렌더링해야 할 때 유용합니다.

```html
<div id="app">
  <ul>
      <li v-for="index in 100">
          {%raw%}{{ index }}{% endraw %}
      </li>
  </ul>
</div>
```
RESULT :
```
1
2
3
4
5
6
7
8
9
...
```
*for in 문법을 for of로 사용해도 똑같이 동작한다.*

#### v-for와 리스트 (Array)

`v-for`는 리스트 데이터에도 적용할 수 있다. 각각의 인덱스 값을 알기 위해 하나의 전달인자를 추가하는 것으로도 값을 얻을 수 있다.

```html
<div id="app">
  <ul>
      <li v-for="(day,index) in days">
          {%raw%}{{ day }}{% endraw %}
      </li>
  </ul>
</div>
```
```js
new Vue({
  el: '#app',
  data: {
    days: ['1122','1108','0409']
  }
})
```
RESULT :
```
1122
1108
0409
```

#### v-for와 오브젝트

오브젝트 데이터를 렌더링하는 방법도 리스트 데이터를 렌더링하는 방법과 유사하다.
오브젝트도 전달인자를 추가하는 것만으로도 키값을 얻을 수 있다.

```html
<div id="app">
    <div v-for="(key,value) in days">
        {% raw %}{{ key }} : {{ value }}{% endraw %}
    </div>
</div>
```
```js
new Vue({
  el: '#app',
  data: {
    userInfo: {
        name : 'gaeng',
        age : 20
    }
  }
})
```
RESULT :
```
 name : gaeng
 age : 20
```


#### key

잦은 DOM 조작은 브라우저의 성능을 급격하게 저하시킨다. 리스트에 렌더링 되는 아이템들의 변경이 자주 발생한다면
병목구간이 생길 수 있다. `key`는 이 부분에 대해 최적화를 할 수 있는 디렉티브이다.
매번 다시 DOM을 렌더링하는게 아니라 겹치는 부분을 재활용할 수 있도록 하는것이 성능에 큰 도움이 될 것이다.

<div id="app">
  <ul>
      <li v-for="(day,index) in days" :key="index"> <!--고유값으로 쓸 것이 없으면 인자를 하나더 받아 key로 사용한다.-->
          {%raw%}{{ day }}{% endraw %}
      </li>
  </ul>
</div>

*Thanks to*

[도서 Vue.js 이정도는 알아야지](http://www.yes24.com/Product/Goods/56894866)  