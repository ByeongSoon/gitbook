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

모든 리소스는 고유한 주소가 존재하고, 서버에 존재한다. 우린 URI를 통해 리소스를 구분하고 호출한다.

**2. 행위 (Verb) - HTTP Method**

웹에서 일어나는 행위는 뻔하지 않은가? CRUD를 말하는 것이다. 그에 맞게 HTTP Method를 설정해주면 된다.

| HTTP Method | 설명                                                            |
| ----------- | ------------------------------------------------------------- |
| POST        | CREATE 작업에 대한 Method로 주로 서버에 데이터를 추가할 때 사용한다.                 |
| GET         | READ 작업에 대한 Method로 주로 서버에서 데이터를 읽어올 때 사용한다.                  |
| PUT         | UPDATE 작업에 대한 Method로 주로 서버 데이터의 갱신을 위해 사용한다. (대상 데이터가 전체일 때) |
| PATCH       | UPDATE 작업에 대한 Method로 주로 서버 데이터의 갱신을 위해 사용한다. (대상 데이터가 일부일 때) |
| DELETE      | DELETE 작업에 대한 Method로 주로 서버 데이터의 삭제을 위해 사용한다.                 |

**3. 표현 (Representation of Resource)**

브라우저와 웹 서버간 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등있다. JSON, XML을 통해 데이터를 주고 받는 것이 일반적이다. 필자는 JSON을 대체로 사용한다.
