---
description: Java의 stream method 중에서 `map`과 `flatmap`의 차이점을 알아본다.
---

# stream method 중 map과 flatmap 차이점

#### map()

.map()은 단일 스트의 원소를 매핑 시킨 후 매핑 시킨 값을 다시 스트림으로 변환하는 중간 연산을 담당다. 객체에서 원하는 원소를 추출하는 역할을 한다고 말할 수 있다.

#### flatmap()

.flatMap()은 Array나 Object로 감싸져 있는 모든 원소를 단일 원소 스트림으로 반환다. .map()은 입력한 원소를 그대로 스트림으로 반환하지만 .flatMap()은 입력한 원소를 가장 작은 단위의 단일 스트림으로 반환한.

