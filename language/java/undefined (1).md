---
description: 디자인 패턴 중에서 싱글톤 패턴에 대하여 알아본다.
---

# 싱글톤 패턴과 사용법

객체를 생성할 때 하나의 인스턴스만 존재해야되는 경우가 몇가지 있다.&#x20;

예를들면 사무실의 프린트, 커피머신 등이 있겠다.

**Single Thread** 에서는 문제가 없지만 **Multi Thread** 에서는 접근시에 여러 개의 객체가 생성될 수 있기 때문에 문제가 발생한다.

싱글톤 패턴의 여러가지 해법이 있지만 이번 글에서는 LazyHolder를 이용한 방법을 소개한다.

```
public class CoffeeMachine {

  private CoffeeMachine() {
    System.out.println("wisoft 커피자판기 입니다.");
  }

  public static CoffeeMachine getInstance() {
    return LazyHolder.INSTANCE;
  }

  private static class LazyHolder {
    private static final CoffeeMachine INSTANCE = new CoffeeMachine();
  }
}
```

위의 코드처럼 객체의 생성을 CoffeeMachine의 getInstance()를 통해서한다. 객체가 필요할 때까지 초기화를 미루는 것이다.

Class를 로딩하고 초기화하는 시점에는 Thread Safe가 보장되기 때문에 다른 방법들 처럼 synchronized가 필요하지 않다.

LazyHolder 방법은 Java 버전도 상관이 없고, 성능또한 뛰어나서 현재까지 가장 완벽하다는 평가를 받고있다.
