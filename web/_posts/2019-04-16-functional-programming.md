---
layout: post
title: "함수형 프로그래밍"
description: >
  함수형 프로그래밍을 알아보자
category: Web Front-end
---
# 함수형 프로그래밍 (Functional Programming)

## 👉 함수형 프로그래밍이란?

함수형 프로그래밍은 순수한 함수를 작성하고, 공유된 상태와 변경 가능한 데이터 및 부작용을 피하여 소프트웨어를 작성하는 프로세스이다.
함수형 프로그래밍은 선언형 프로그래밍이며, 애플리케이션의 상태는 순수한 함수를 통해 전달된다.애플리케이션의 상태가 공유되고,
객체의 메소드와 사용되는 객체지향 프로그래밍과는 *대조*된다.

#### 명령형 프로그래밍과의 비교

![명령형 프로그래밍과의 비교](/assets/images/functional/compare.jpg)

## 🙄 왜 함수형 프로그래밍을 배워야할까

![FUNCTIONAL PROGRAMMING](/assets/images/functional/functional.png)

>"일반적은 프로그래밍은 그냥 생각하면 되는것이고, **함수형 프로그래밍은 기존과 다르게 생각하는 방법**을 알려 줄 것이다.
>그러므로 당신은 아마도 예전의 방식으로 절대 돌아가지 않을 것이다."

함수형 프로그래밍은 프로그래밍 언어나 방식을 배우는것이 아니라 함수로 프로그래밍하는 사고를 배우는것이라고 할 수 있다.
즉, 사고의 전환이 필요하고, 다양한 사고방식으로 프로그래밍을 바라보면 유연한 문제 해결이 가능해진다.
명령형이나 객체지향 코드보다 간결하고 예측하기 쉬우며, 테스트하기가 더 쉬워진다. 

## 👉 함수형 프로그래밍에 필요한 개념

#### 1급 객체(First Object, 1급 시민)

- 1급 객체란 다음 조건을 만족하는 객체
    - 변수나 데이터를 구조 안에 담을 수 있다.
    - 파라미터로 전달 할 수 있다.
    - 반환값으로 사용할 수 있다.
    - 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다.
    - 동적으로 프로퍼티 할당이 가능하다.

#### 고차함수(Higher-Order Function)
- HOC(Higher-Order Function)는 다른 함수를 인자로 사용하거나 함수를 반환하는 함수, 또는 두가지 특징을 모두 가진 함수이다.HOC는 다음과 같은 경우 주로 사용된다.
    - 콜백함수, 프로미스, 모나드 등을 사용하여, 동작과 효과 또는 비동기 흐름 제어를 추상화하거나 격리한다.
    - 다양한 데이터 유형에 대해 작동할 수 있는 유틸리티를 생성한다.
    - 함수를 부분적으로 인수에 적용하거나 재사용 또는 함수 조합을 위한 커리 함수를 작성한다.
    - 함수 목록을 가져오고, 해당 입력 함수의 조합을 반환한다.


#### 불변성(immutability)

- 함수형 프로그래밍에서는 데이터가 변할 수 없는데, 이를 불변성 데이터라고 한다.
- 데이터 변경이 필요한 경우, 원본 데이터 구조를 변경하지 않고 그 데이터의 복사본을 만들어 그 일부를 변경하고, 변경한 복사본을 사용해 작업을 진행한다.

>자바스크립트의 `const` 키워드는 Object로 사용되는 경우 변경 가능하다.
>이를 방지하기 위해 `Immutable.js` 등의 라이브러리를 사용하거나, `Object.freeze` 메소드를 사용 할 수 있다.

```js
// 불변이 아닌 변하는(Mutatable) 데이터
function rateColor(color, rating) {
  color.rating = rating;
  return color;
}

console.log(rateColor(color_lawn, 5), rating) // 5
console.log(color_lawn.rating) // 5

// 불변성 데이터
function rateColor(color, ratring) {
  return Object.assign({}, color, {ratring:ratring});
}

console.log(rateColor(color_lawn, 5), rating) // 5
console.log(color_lawn.rating) // 0  *변하지 않음*
```

#### 순수 함수(Pure functions)

- 함수형 프로그래밍에서 중요한 핵심은 함수는 부작용이 없어야 하며, 외부상태에 종속되지 않아야 한다.
- 함수는 입력을 받고 출력을 반환함에 있어 외부의 값에 접근하지 않아야 한다.

```js
//순수함수의 예시
/* 순수 함수 */
const double = num => (num * 2);
/* 순수하지 않은 함수 */
const operand = 2;
const multiple = num => (num * operand);
```

#### 합성 함수 (Function composition)

- 합성 함수란 새로운 함수를 만들거나 계산하기 위해 둘 이상의 함수를 조합하는 과정을 말한다.
- 함수형 프로그래밍은 여러 작은 순수함수들로 이루어져있기 때문에 이 함수들을 연쇄적으로 또는 병렬로 호출해서 더 큰 함수를 만드는 과정으로 전체 프로그램을 구축해야 한다.

```js
// 합성함수의 예시
const compose = (f, g) => x => f(g(x));
const add = x => y => x + y;
const pow = x => y => y ** x;
const add2 = add(2);
const square = pow(2);
const add2ThenSqaure = compose(square, add2);
add2ThenSquare(10); // 144 

```


#### 재귀(Recursion)
- 함수형 프로그래밍에서는 반복문 대신 재귀를 사용한다.
- 기존의 어떤 값을 수정하는 것이 아니라, 기존값으로 새로운 값을 계산하고 이를 사용한다.
- 반복문을 대체할 수 있을 뿐만 아니라, `분할 및 정복` 알고리즘을 구현하는데 매우 유용하다.

```js
//함수형 프로그래밍에서의 재귀함수 예시

/* sum 1..10 with loop */
let sum = 0;
for (let i = 1; i <= 10; i++) {
  sum += i + 1;
}
console.log(acc); // 55
/* sum 1..10 with recursion */
sumRange = ({ start, end }) =>
  (sum) => {
    if (start > end) {
      return sum;
    }
    return sumRange({ start: start + 1, end })(sum + start);
  };
sumRange({ start: 0, end: 10 })(0);
```

##### 대표적인 재귀 함수의 사용 예시 - 팩토리얼

```js
const factorial = n =>
  n ?
    n * factorial(n - 1) :
    1;
```

#### 모나드(Monads)

**Monad**는 `of`와 `chain`이 있는 객체이다.(`chain`은 중첩된 객체를 un-nenesting하는 점을 제외하면, map과 같다.)

```js
// Implementation
Array.prototype.chain = function (f) {
  return this.reduce((acc, it) => acc.concat(f(it)), []);
}
// Usage
Array.of('cat,dog', 'fish,bird').chain(e => e.split(',')); // ['cat', 'dog', 'fish', 'bird']
// Difference with map
Array.of('cat,dog', 'fish,bird').map(e => e.split(',')); // [['cat', 'dog'], ['fish', 'bird']]
```

#### 커링(Currying)
커링은 여러 인자를 받는 함수를 인자 하나씩 사용하여 함수 순서를 실행할 수 있도록 변환하는 것을 말한다.
이는 람다 표현식과 클로저를 통해 쉽게 구현할 수 있다.

```js
//커링 예시
/* not curried function */
function sumOfThreeThings(x, y, z) {
  return x + y + z;
}
sumOfThreeThings(1, 2, 3); // 6
/* curried function */
const sumOfThreeThings = x =>
  y =>
    z =>
      x + y + z;
sumOfThreeThings(1)(2)(3); // 6
```
*Thanks to*

[참고 : kyusung - 함수형-프로그래밍-요약](https://velog.io/@kyusung/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9A%94%EC%95%BD)

[참고 : yocee57 - 함수형 프로그래밍이란?](https://medium.com/korbit-engineering/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B4%EB%9E%80-e7f7b052411f)