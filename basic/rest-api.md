---
description: REpresentational State Transfer
---

# REST API

> REST는 WWW(World Wide Web)과 같은 분산 하이퍼 미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식이다. 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.

API를 구축할때 URI와 HTTP Method를 활용하여 API의 기능을 추측 가능하게끔 아키텍쳐를 구성하는 원칙같은 것이다. REST 원칙을 잘 따른 API만이 RESTful API로 부를 수 있다.&#x20;

{% hint style="info" %}
REST full API란?

REST의 원리를 따르는 시스템을 의미하며 REST를 사용했다고 모두가 RESTful 한 것은 아니다.&#x20;

REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful 하다고 말할 수 있다.
{% endhint %}

### REST 구성 요소

**1. 자원 (Resource) - URI**

모든 자원에는 고유한 주소가 존재하고, 서버에 존재한다. 우린 URI를 통해 자원을 구분하고 호출한다.

**2. 행위 (Verb) - HTTP Method**

웹에서 일어나는 행위는 CRUD를 말하는 것이다. 그에 맞게 HTTP Method를 설정해주면 된다.

| HTTP Method | 설명                                   |
| ----------- | ------------------------------------ |
| POST        | 서버에 데이터를 추가할 때 사용한다.                 |
| GET         | 서버에서 데이터를 읽어올 때 사용한다.                |
| PUT         | 서버 데이터의 갱신을 위해 사용한다. (대상 데이터가 전체일 때) |
| PATCH       | 서버 데이터의 갱신을 위해 사용한다. (대상 데이터가 일부일 때) |
| DELETE      | 서버 데이터의 삭제을 위해 사용한다.                 |

**3. 표현 (Representation of Resource)**

브라우저와 웹 서버간 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있다. JSON, XML을 통해 데이터를 주고 받는 것이 일반적이다. 필자는 JSON을 대체로 사용한다.

### REST 특징

**1. 서버-클라이언트 구조 (Server-Client) :** 서버와 클라이언트 구조를 띈다는 것이다.

**2. 무상태 (Stateless) :** HTTP 프로토콜을 사용하기 때문에 HTTP의 특징인 무상태성을 갖는다.

**3. 캐시 처리 가능 (Cacheable) :** HTTP 프로토콜의 Last-Modified Tag 또는 E-Tag를 이용해 캐싱을 지원한다.

**4. 계층화 (Layered System) :** 클라이언트, 서버로만 구성할 수 도 있고 중간에 Gateway나 프록시 서버와 같은 미들 웨어를 배치해 계층화 할 수 있다.

**5. 인터페이스 일관성 (Uniform Interface) :** URI로 지정한 리소스에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍처 스타일을 의미한다.

**6. 자체 표현 (Self-Descriptiveness) :** URI만 분석해도 무슨 기능인지 유추가 된다.

{% hint style="info" %}
#### HTTP란?

[https://velog.io/@carrotsman91/HTTP-RequestResponse](https://velog.io/@carrotsman91/HTTP-RequestResponse)
{% endhint %}

### REST 장단점 <a href="#rest" id="rest"></a>

#### **장점** <a href="#rest" id="rest"></a>

* HTTP 인프라 베이스라서 REST API를 위한 인프라를 별도로 구축할 필요가 없다.
* HTTP 표준을 따르기 때문에 HTTP의 여러 추가적인 기능을 사용할 수 있다.
* HTTP를 지원하는 모든 플랫폼에서 사용이 가능하다.
* Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
* REST API URI를 통해서 의도하는 바를 명확하게 나타내므로 기능을 쉽게 파악할 수 있다.
* 기능 통합으로 여러 서비스를 통합할 때 생기는 디자인 문제를 최소화한다.
* 서버와 클라이언트의 역할을 명확하게 분리한다.

**단점**

* 표준 자체가 존재하지 않아 정의가 필요하다.
* HTTP Method 형태가 제한적이다. (GET, POST, PUT, PATCH, DELETE 등)
* 테스트에 있어 전문성을 요구한다. (Header, dataType 등 HTTP 부가정보 설정 필요)
* 구형 브라우저에서 호환이 되지 않아 지원해주지 못하는 동작이 많다.



### REST API 설계 규칙 <a href="#rest-api" id="rest-api"></a>

**1. URI는 동사 보다는 명사를, 대문자 보다는 소문자를 사용한다.**

```
https://velog.io/@carrotsman91/shit
```

**2. 마지막에 슬래시(/)를 포함하지 않는다.**

```
https://velog.io/@carrotsman91/shit
```

**3. 언더바(\_) 대신 하이픈(-)를 사용한다.**

```
https://velog.io/@carrotsman91/carrots-shit
```

**4. URI는 행위를 포함하지 않는다.**

```
https://velog.io/@carrotsman91/carrots/1
```

**5. 파일확장자는 URI에 포함하지 않는다.**

```
https://velog.io/@carrotsman91/carrotsShit
```
