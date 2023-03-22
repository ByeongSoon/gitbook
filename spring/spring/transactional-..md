---
description: 백엔드 개발 시 트랜잭션 처리를 위해 흔히 사용하는 @Transactional 어노테이션에 대해 알아보자.
---

# @Transactional에 대해서 설명해주세요.

#### @Transactional은 Spring AOP의 대표적인 예다.

* 즉, 프록시로 동작하므로 오버라이딩 개념으로 동작한다.
* 메서드에 @Transactional을 붙이면 해당 클래스가 빈으로 등록될 때 @Transactional이 붙은 메서드만 트랜잭션 처리되는 메서드로 오버라이딩 한 프록시 객체가 빈으로 등록된다. 클래스에 붙으면 클래스의 전체 public 메서드에 트랜잭션 처리가 된 프록시가 빈으로 등록된다.
* public이 아닌 다른 접근제한자가 붙은 메서드의 경우는 트랜잭션처리가 되지 않는데 이유는 프록시가 오버라이딩 개념이기 때문에 public으로 열려있지 않고 private 메서드 같은 경우에는 적용이 불가능하다.

#### 내부 호출 문제

* @Transactional이 붙은 클래스는 프록시로 빈으로 등록된다.\
  따라서 주입받은 객체를 사용할 경우 프록시가 들어오게 되고 접근 시 프록시 객체를 통한 호출이 이뤄진다.

```java
public class UserService {

    @Transactional
    public void createUserListWithTrans(){
        for (int i = 0; i < 10; i++) {
            createUser(i);
        }
            
        throw new RuntimeException(); 
    }

    @Transactional
    public User createUser(int index){
        User user = User.builder()
                .name("testname::"+index)
                .email("testemail::"+index)
                .build();
        
        userRepository.save(user);
        return user;
    }
}
```

* `createUserListWithTrans()`에서 `createUser()`를 호출한다.&#x20;
* 둘다 @Transactional이 붙어있기에 `createUser()`에서 `save()` 처리를 했으므로 예외가 발생하더라도 다 저장되었을 것이라고 생각할 수 있지만 틀렸다.
* 이유는 트랜잭션이 붙은 상태로 동작하려면 프록시를 통해 접근해야 하는데 위는 실제 코드를 호출한 것이기 때문
* `createUserListWithTrans()`를 호출할 경우 아래와 같이 프록시 객체로 동작한다.

```java
public void createUserListWithTrans(){
    EntityTransaction tx = em.getTransaction();
    tx.begin();
    
    super.createUserListWithTrans();
    
    tx.commit();
}
```

* `createUserListWithTrans()`에 붙은 @Transactional만 동작하게 된다.
* 즉, 하나의 트랜잭션 안에서 동작하게 되는 것이다. 만약 트랜잭션이 붙은 프록시를 호출해서 사용하다가 다른 트랜잭션이 붙은 프록시 클래스를 호출할 경우 이때부터는 트랜잭션 전파 속성에 따라 트랜잭션이 동작한다.\

* 진입점에 Trasactional이 없고 안에서 호출되는 메서드에만 Transactional이 있는 경우

```java
public class UserService {

    public void createUserListWithTrans(){
        for (int i = 0; i < 10; i++) {
            createUser(i);
        }
            
        throw new RuntimeException(); 
    }

    @Transactional
    public User createUser(int index){
        User user = User.builder()
                .name("testname::"+index)
                .email("testemail::"+index)
                .build();
        
        userRepository.save(user);
        return user;
    }
}
```

* Userservice는 `createUser()`에 붙은 @Transactional 때문에 프록시가 빈으로 등록된다.
* userService는 프록시이지만 `createUserListWithTrans()`는 트랜잭션이 붙어있지 않으므로 트랜잭션 처리되지 않는 것을 호출하게 되고, 내부적으로 `createUser()`을 호출하게 되어 트랜잭션 없이 호출하게 된다.
  * 실행결과를 보면 user 10개 생성되게 되는데 이는 @Transactional이 없기 때문에 `createUser()`가 각각 insert하면서 DB의 기본 설정대로 auto commit이 true로 인한 동작 결과이다.
  * @Transactional은 auto commit을 false로 하고 마지막에 commit한다.





* 참고 : [https://github.com/backtony/Backend\_Interview\_for\_Beginner/blob/master/Spring%20%26%20JPA.md](https://github.com/backtony/Backend\_Interview\_for\_Beginner/blob/master/Spring%20%26%20JPA.md)
