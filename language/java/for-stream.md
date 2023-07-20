---
description: 반복된 작업을 필요로하는 경우에 사용할 수 있는 반복문과 stream의 차이점은?
---

# for문과 stream의 차이점은?

### 등장

* for문은 java 1, for-each문은 Java 5부터 등장했습니다.
* stream은 함수형 프로그래밍 패러다임이 도입된 Java 8부터 등장했습니다.

### 차이점

* 익숙함의 차이에서 오는 가독성의 호불호가 있다.
* 디버깅 난이도의 차이가 있다.
  * for : 에러 발생 위치가 바로 노출된다.
  * stream : 지연 연산을 통해 실행되기에 에러 발생 시 위치를 따로 추적해야 한다.
* 병렬 처리 구현의 차이가 있습니다.
  * for 구체적인 로직을 나누어 구현하고 합쳐야 한다.
  * stream parallelStream()으로 쉽게 처리한다.

### 성능차이

{% hint style="info" %}
primitive/array에서는 차이가 있지만, wrapper/collection에서는 큰 차이가 없다.
{% endhint %}

* stream이 for문보다 늦게 나왔기 때문에 stream은 for문에 비해 최적화가 잘 이루어지지 않았다.
* stream은 for문에 비해 오버헤드가 발생합니다.
  * stream 사용을 위해서는 boxing이 필요하지만, for문은 인덱스에 바로 접근하여 오버헤드가 발생하지 않습니다.
  * 하지만 프로덕션 코드에서는 boxing된 collection이 주로 사용되기에 큰 차이는 아니라고 생각합니다.

### 참고

{% embed url="https://hyune-c.tistory.com/entry/for-vs-stream" %}
