---
description: Java에서 메모리를 자동으로 관리해주는 가비지 컬렉션에 대해서 알아보자.
---

# 가비지 컬렉션이란?

### 가비지 컬렉션이란? <a href="#garbage-collection" id="garbage-collection"></a>

* 가비지 컬렉션은 JVM의 메모리 관리 기법 중 하나로 시스템에서 동적으로 할당되었던 메모리 영역 중에서 필요 없어진 메모리 영역을 회수하여 메모리를 관리해주는 기법

### 가비지 컬렉션 과정 <a href="#undefined" id="undefined"></a>

* GC의 작업을 수해하기 위해서는 JVM이 어플리케이션의 실행을 잠시 멈춤
* GC를 실행하는 스레드를 제외한 모든 스레드들의 작업을 중단 후(Stop The World 과정) 사용하지 않는 메모리를 제거(Mark and Sweep)
* 중단했던 스레드들의 작업 재개
