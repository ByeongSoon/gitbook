---
description: 스프링 IoC 컨테이너를 통해 자동으로 의존성 주입을 해줄때 같은 타입일 경우에 어떻게 해결하는지 알아보자.
---

# 같은 인터페이스의 구현체 클래스 두 개 이상이 빈으로 등록되면 어떻게 의존성을 주입 할 수 있는가?

Spring Boot에서 어노테이션을 통해 자동으로 빈을 컨테이너에 설정하는 경우, 같은 인터페이스의 구현체 클래스 두 개 이상이 빈으로 등록되면 아래와 같은 Exception이 발생한다.

> NoUniqueBeanDefinitionException: No qualifying bean of type 'test.a' available: expected single matching bean but found 2

### 예시 코드

```java
public interface Video {
    String play();
}

@Component
public class Netflix implements Video {
    public String play() {
	return "Netflix";
    }
}
@Component
public class Youtube implements Video {
    public String play() {
	return "Youtube";
    }
}

@Service
public class VideoService {
    private final Video video;
	
    @Autowired
    public VideoService(Video video) {
	this.video = video;
    }
}
```

### Autowired된 필드의 이름을 빈 이름으로 설정하는 방법

* @Autowired로 생성자에 주입되는 Video 객체의 변수명을 구현체 클래스의 이름인 netflix으로 만들면,&#x20;
* Video 클래스의 빈이 두 개인 것을 확인한 Spring Boot가 netflix 이름과 같은 빈이 있는지 찾아서 주입해준다.

```java
@Service
public class VideoService {
    private final Video netflix;
	
    @Autowired
    public VideoService(Video video) {
	this.video = video;
    }
}
```

### @Qulifier 어노테이션을 사용하는 방법

* Qualifier 어노테이션은 빈에 추가 구분자를 붙여주는 방법으로 생성자에서 해당 구분자를 명시하면 그 구분자를 가진 빈을 주입해준다.&#x20;
* 헷갈리기 쉬운 점은 Qualifier가 빈 이름을 변경한다고 생각할 수 있는데, 빈 이름은 그대로 있고 추가적으로 구분자가 생기는 것이다.
* 생성자 자동주입말고도 수정자 주입에서도 같은 방식으로 사용할 수 있다.

```java
@Component
@Qualifier("netflixVideo")
public class Netflix implements Video {
    public String play() {
        return "Netflix";
    }
}
@Component
@Qualifier("youtubeVideo")
public class Youtube implements Video {
    public String play() {
        return "Youtube";
    }
}

@Service
public class VideoService {
    private final Video video;
	
    @Autowired
    public VideoService(@Qualifier("youtubeVideo") Video video) {
    	this.video = video;
    }
}
```

### @Primary 어노테이션을 사용하는 방법

* 가장 간단한 방법으로 여러 빈이 있을 때 기본적으로 선택될 빈에 @Primary 어노테이션을 붙여주면 자동적으로 해당 빈이 선택된다.&#x20;
* 주입 받을 때마다 모든 코드에 @Qualifier 어노테이션을 붙여줘야하는 Qualifier 방법보다 간단하다.
* 메인 기능으로 사용되는 빈과 서브 기능으로 가끔 사용되는 빈이 있을 때 메인 기능으로 사용하는 빈에 @Primary를 적용하고, 서브 기능으로 사용하는 빈을 사용할 때는 @Qualifier를 명시적으로 지정하여 주입하면 두 어노테이션의 장점만을 각각 사용할 수 있다.

```java
@Component
@Primary
public class Netflix implements Video {
    public String play() {
        return "Netflix";
    }
}
@Component
@Qualifier("youtubeVideo") // @Primary와 함께 사용가능
public class Youtube implements Video {
    public String play() {
        return "Youtube";
    }
}

@Service
public class VideoService {
    private final Video video;
	
    @Autowired
    public VideoService(Video video) {
    	this.video = video;
    }
}
```

### @Qualifier와 @Primary의 우선순위

*   스프링은 기본적으로 자동보다 수동으로 지정한 것이 높은 우선 순위를 갖는다. 따라서 자동적으로 빈을 선택해주는 @Primary보다 명시적으로 지정하는 @Qualifier 어노테이션이 우선 순위를 가진다.



### 참고

{% embed url="https://bestinu.tistory.com/58" %}
