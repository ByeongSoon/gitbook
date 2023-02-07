---
description: 흔히 서버 개발을 하면서 사용하는 HTTP 메서드의 종류와 각 메서드의 역할을 알아본다.
---

# HTTP 메서드와 각 메서드의 역할은?

### REST(Representational State Transfer)란?

* 자원(Resource) : URI
* 행위(Verb) : HTTP Method
* 표현(Representations)

REST에서 행위에 해당하는 HTTP Method는 대표적으로 CRUD에서 이용한다.



### HTTP Method 종류

* GET : 서버에서 리소스 조회
* POST : 요청 데이터 서버에 등록
* PUT : 서버의 데이터 수정. 해당 리소스가 없으면 생성.
* PATCH : 서버의 데이터 부분 변경(PUT은 전체 수정)
* DELETE : 서버의 데이터 삭제
* HEAD : 리소스 조회지만 상태와 헤더(메타데이터)만 반환
* OPTIONS : 리소스가 지원하고 있는 HTTP 메서드 반환
* CONNECT : 프록시 동작의 터널 접속을 변경



### 기타

* 데이터를 BODY에 담는 POST 방식이 URL에 데이터 정보가 노출된 GET 방식보다 보안 측면에서 조금 더 안전하다고 볼 수 있다.
* GET 방식은 캐싱을 하기 때문에 여러번 요청 시 캐싱 된 데이터를 사용하기 때문에 다른 메서드에 비해서 빠를 수 있다.
* POST는 새로운 데이터를 등록(생성)할 때 사용하고, PUT은 사용자 정보를 수정할 때 사용한다.
* PUT은 지정한 데이터를 전부 수정하는 메서드이고, PATCH는 정보의 일부분이 변경되는 방법이다.
