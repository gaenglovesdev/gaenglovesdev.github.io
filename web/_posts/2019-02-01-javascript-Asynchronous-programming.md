---
layout: post
title: "자바스크립트 비동기 프로그래밍"
description: >
  자바스크립트 비동기 프로그래밍에 대해 설명합니다.
category: Web Front-end
---

# 자바스크립트 비동기 프로그래밍(Promise , Async Await)

## 🔎동기와 비동기 알아보기

![동기와 비동기](/assets/images/asynchronous/block_nonblock.png)

#### 동기란(synchronous)?

Synchronous란 '요청과 그 결과가  동시에 일어난다'라는 뜻이다.

요청에 따른 응답이 동시에 일어난다는 것을 뜻하며,

직렬적으로 태스크(task)를 수행한다.

즉, 태스크는 순차적으로 실행되며 어떤 작업이 수행 중이면 다음 작업은

대기하게 된다.

![동기식 처리 모델](/assets/images/asynchronous/synchronous.png)



#### 비동기란(asynchronous)?
Asynchronous는 '요청과 그 결과가 동시에 일어나지 않는다'라는 뜻이다.

비동기는 병렬적으로 태스크를 수행한다.

즉, 태스크가 종료되지 않은 상태라 하더라도 대기하지 않고

다음 태스크를 실행한다


![비동기식 처리 모델](/assets/images/asynchronous/synchronous.png)


## Promise🤙

>Single thread인 javascript는 비동기 처리를 위해 콜백 패턴을 사용해왔다.
>하지만 전통적인 콜백 패턴은 가독성이 나쁘고 비동기 처리 중 발생한 에러의 예외 처리가 곤란하며
>여러 개의 비동기 처리 로직을 한꺼번에 처리하는 것도 한계가 있다. ES6에서 비동기 처리를 위한 또 다른 패턴으로 프로미스(Promise)를 도입하였다.


#### 콜백 패턴의 단점 1 : 콜백 헬
비동기 처리를 위해 콜백 패턴을 사용하면 처리 순서를 보장하기 위해 여러 개의 콜백 함수가 네스팅(nesting, 중첩)되어
복잡도가 높아지는 *콜백 헬(Callback Hell)*이 발생하는 단점이 있다.
콜백 헬은 가독성을 나쁘게 하며 실수를 유발하는 원인이 된다.
```js
//콜백함수의 콜백헬 예시
step1(function(value1) {
  step2(value1, function(value2) {
    step3(value2, function(value3) {
      step4(value3, function(value4) {
        step5(value4, function(value5) {
            ...
        });
      });
    });
  });
});
```

#### 콜백 패턴의 단점 2 : 에러 처리
또한 콜백방식의 비동기 처리방식의 치명적인 단점은 *에러 처리가 곤란*하다는 것이다.
`try-catch` 스코프 내에서 콜백함수의 에러를 캐치하지 못한다는 담점이 있다.
예외(exception)가 호출자(caller) 방향으로 전파되는데 비동기 함수 호출자는 콜 스택에서 이미 사라졌기 때문이다.


#### 프로미스의 상태
생성된 프로미스 객체는 다음과 같은 상태값을 갖는다.
- Pending(대기) : 비동기 처리 로직이 완료되지 않은 상태  
- Fullfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태
- settled : pending이 아닐 때를 말하며, 결론이 난 상태


#### 프로미스의 선언
```js
  //프로미스 생성
  const getData = function(state){
    return new Promise((resolve,reject) => {
      if(state){
        resolve()
      }else{
        reject()
      }
      
    })
  }

  getData(true)
    .then(response => {
      //Logic
    })
    .catch(error => {
      //Logic
    })
```
*프로미스의 생성*은 `Promise` 생성자 함수를 통해 인스턴스화 한다. `Promise` 생성자 함수는 비동기 작업을 수행할
콜백 함수를 인자로 전달받는데 이 콜백 함수는 `resolve`와 `reject`함수를 인자로 전달받는다.

*프로미스의 후속 처리 메소드*는 두가지로 아래와 같다.
- then() : 두 개의 콜백 함수를 인자로 전달 받는다. 첫번쨰 콜백 함수는 성공 시 호출되고, 두번째 함수는 실패시 호출된다.
- catch() : 예외가 발생하면 호출된다.



## Async/Await
프로미스 패턴이 콜백 지옥을 벗어날 수 있게 해줬다고 하지만 역시나 코드가 길어지면 프로미스 패턴역시
가독성이 떨어진다. 이에 es8에서는 es6의 `generator`와 비슷한 모습인 `Async/Await`를 도입하여 비동기코드의 겉모습을
좀 더 동기 코드와 유사하게 만들었다.

#### 특징

- funtion 키워드 앞에 `async`를 붙여주고 비동기로 처리되는 부분 앞에 `await`를 붙여준다.
- await은 반드시 promise를 반환해야 한다.

```js
//선언
async function something(data1){
  const data2 = await gaeng1(data1);
  const data3 = await gaeng1(data2);
  const data4 = await gaeng1(data3);
}
//호출
something(data)
```

#### 에러 처리

`async / await`은 동기와 비동기 에러를 모두 `try/catch`를 통해서 처리할 수 있게 한다.
*Thanks to*

[참고 : Poiemaweb - Promise](https://poiemaweb.com/es6-promise)
[참고 : constell99 - 자바스크립트의 Async/Await 가 Promises를 사라지게 만들 수 있는 6가지 이유](https://medium.com/@constell99/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-async-await-%EA%B0%80-promises%EB%A5%BC-%EC%82%AC%EB%9D%BC%EC%A7%80%EA%B2%8C-%EB%A7%8C%EB%93%A4-%EC%88%98-%EC%9E%88%EB%8A%94-6%EA%B0%80%EC%A7%80-%EC%9D%B4%EC%9C%A0-c5fe0add656c)
