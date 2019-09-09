---
layout: post
title: "REST, REST API, RESTFUL"
description: >
  REST,REST API,RESTFUL를 알아보자
category: Web
---
### REST, REST API, RESTFUL

## REST
---

#### 👉 REST란?
- **Representational State Transfer** 의 약자로 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
- 자원의 이름(대표 혹은 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.
- 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
- JSON or XML을 통해 데이터를 주고받는것이 일반적이다.
- 데이터가 요청되는 시점에서 자원의 상태(정보)를 전달한다.
- HTTP URI를 통해 자원을 명시하고 HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는것을 의미한다. 


#### 👉 REST의 장단점
- 장점
    - HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없다.
    - HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다(다양한 클라이언트에 대응가능).
    - Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
    - 서버와 클라이언트의 역할을 명확하게 분리한다.

- 단점
    - 표준이 존재하지 않는다.
    - 사용할 수 있는 Method가 4가지로 제한된다.
    - 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
    

#### 👉 REST의 구성요소
- 자원(Resource) : URI
    - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다
    - 자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.
    - Client URI를 이요해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다
- 행위(Verb) : HTTP Method
    - HTTP 프로토콜의 Method를 사용한다
    - HTTP 프로토콜은 **GET, POST, PUT, DELETE**와 같은 메서드를 제공한다.
- 표현(Representation of Resource)
    - Client가 자원의 상태에 대한 조작을 요청하면 Server는 이에 적절한 응답을 보낸다.
    - REST에서 하나의 자원은 **JSON, XML, TEXT, RSS**등 여러 형태의 Representation으로 나타내어 질 수 있다.


#### 👉 REST의 특징
- Server-Client 구조
    - 자원이 있는 쪽이 Server , 요청하는쪽이 Client
    - 구조가 나누어지므로 서로간의 의존성이 줄어든다.
- Stateless
    - HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
    - client의 context 정보(세션,쿠키)를 신경쓰지 않아도 되므로 구현이 단순해진다.
- Cacheable
    - HTTP 프로토콜을 사용하기 때문에 캐시처리가 가능하다.
    - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
    - 캐시사용을 통해 전체응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
- Layered System
    - Client는 REST API Server만 호출한다.
    - 프록시, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
- Code-on-Demand(optional)
    - Server로부터 스크립트를 받아서 Client에서 실행한다.
    - 반드시 충족할 필요는 없다.
- Uniform Interface
    - URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.(특정 언어,기술에 종속 X)

## REST API
---

#### 👉 REST API란
- REST를 기반으로 서비스 API를 구현한 것
- 최근 OpenAPI, 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.


#### 👉 REST API의 특징
- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
- 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.


#### 👉 REST API 설계 기본 규칙
- URI는 정보의 자원을 표현해야 한다.
    - resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
    - resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다.
    - resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다.
    - resource의 스토어 이름으로는 복수 명사를 사용해야 한다.

- 자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
    - URI에 HTTP Method가 들어가면 안된다.
    - URI에 행위에 대한 동사 표현이 들어가면 안된다
    - 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.

*(이하 자세한 설계 규칙에 대해서는 차후 포스팅에서 자세히 다룹니다.)*


## RESTful
---

#### 👉 RESTful이란
- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 공식적인것은 아니다.

#### 👉 RESTful의 목적

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.


*Thanks to*

[참고 : gmlwjd9405 - [Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
[참고 : A MEAN Blog - REST와 RESTful API](https://www.a-mean-blog.com/ko/blog/%ED%86%A0%EB%A7%89%EA%B8%80/_/REST%EC%99%80-RESTful-API)
[참고 : poiemaweb - REST(Representational State Transfer) API](https://poiemaweb.com/js-rest-api)