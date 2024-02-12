---
title: "[Spring Boot] 1.스프링 부트 핵심 개념"

toc: true
toc_sticky: true

categories:
   - Spring
tags:
   - Spring
   - Spring Boot

last_modified_at: 2024-02-12T23:00:00




---

# 스프링 부트 핵심 개념

> Spring Boot가 생겨나게 된 배경과 핵심 원리 및 개념에 대해 알아본다

![springboot1]({{site.url}}{{site.baseurl}}/assets/images/springboot/1/springboot1.png)

## 1. Spring Boot 간단소개

> 스프링 부트(Spring Boot)는 스프링을 기반으로 실무 환경에 사용 가능한 수준의 **<u>독립실행형 애플리케이션</u>**을 복잡한 고민 없이 **<u>빠르게 작성할 수 있게 도와주는</u>** 여러가지 도구의 모음이다

### 1-1. 스프링 부트의 핵심 목표

1. 매우 빠르고 광범위한 영역의 스프링 개발 경험을 제공한다
2. 즉시 적용 가능한 기술 조합을 제공하여 필요에 따라 원하는 방식으로 손쉽게 변형 가능하다
3. 내장형 서버, 보안, 외부 설정 방식 등등 프로젝트에서 필요로 하는 다양한 비기능적 기술을 제공한다
4. 코드 생성이나 XML 설정을 필요로 하지 않는다

## 2. Spring Boot 핵심 개념

### 2-1. Containerless

> Spring Boot는 Spring이 Containerless Web Application Architecture를 지원해주면 좋겠다는 어느 한 Spring 개발자의 요청으로부터 출발했다

여기서 **Containerless**는 **Container**가 없다는 뜻이 아니라 **Serverless**와 비슷한 개념이라 생각하면 된다. 이는 Server의 설치와 관리에 신경쓰지 않고 Server 애플리케이션을 개발할 수 있도록 한다

그렇다면 **Container**가 무엇을 의미할까?

![springboot2]({{site.url}}{{site.baseurl}}/assets/images/springboot/1/springboot2.png)

- Web Client가 요청을 보내면 Servlet이 이를 처리한다
- 수많은 Servlet 중 어떤 Servlet이 해당 요청을 처리할지 결정하고 선택하는 과정을 mapping 이라고 하며 Servlet Container가 수행한다
  - 많은 사람들이 알고있는 Tomcat, Jetty이 바로 Servlet Container이다
- Servlet Container만으로는 한계를 느껴 탄생한 것이 바로 Spring이고 Spring Container가 추가되었다
- Spring Container는 Servlet으로부터 요청을 받아 작업을 처리할 Bean을 결정한다
- 과거 Servlet Container를 사용하기 위해 ```web.xml```을 비롯한 수많은 설정들을 적어줘야했다

눈치 빠른 사람들은 이 정도 설명이면 Containerless가 무엇을 의미하는지 알아챘을 것이다

Containerless는 위 그림에서 Servlet Container의 역할을 개발자가 신경쓰지 않아도 되게끔 해준다. 즉, Spring Boot는 **<u>개발자가 매번 번거롭게 Servlet Container 관련 설정을 적어주는 과정을 생략하고 비즈니스 로직에 집중할 수 있도록 돕는다.</u>** 실제로 Spring Boot를 사용하면 SpringApplication 클래스의 main 메서드만 호출하면 전체가 동작하는데 이를 **독립실행형 애플리케이션**이라 부른다

### 2-2. Opinionated

> Spring Boot는 비즈니스 로직을 제외한 나머지 작업들을 관리하여 **<u>개발자가 도메인 핵심 개발에만 집중할 수 있도록</u>** 돕는다

- Spring은 극단적인 유연성을 추구하기 때문에 Not Opinionated를 설계 철학으로 한다. 모든 것을 개발자가 선택하여 설정하도록 하는 것이다
- 반면, Spring Boot는 우선 빠르게 개발하고 그외 설정들은 추후에 진행할 수 있도록 돕는 **Opinionated**의 특성을 지닌다
- Spring Boot는 다양한 기술과 의존 라이브러리 그리고 그들의 버전을 관리해준다
- 또한, **<u>필요하다면 이러한 default 구성값들을 커스터마이징할 수 있도록 유연한 방법을 제공</u>**한다

## 3. Servlet과 Front Controller 그리고 Spring Container

> 기존에 서블릿을 이용하여 Client의 요청과 응답을 처리하던 것을 스프링 부트가 어떻게 단순화시켰는지 알아보자

### 3-1. 서블릿

- 서블릿은 Client의 요청을 받고 그에 대한 응답을 전달해주는 역할을 한다
- Servlet Container가 각각의 요청에 대해 어떤 서블릿이 처리할지를 결정하는데 이를 mapping 이라 한다

### 3-2. 프론트 컨트롤러

> 수많은 서블릿이 가지고 있는 중복 코드 문제를 해결하기 위해 등장한 것이 프론트 컨트롤러이다

![springboot3]({{site.url}}{{site.baseurl}}/assets/images/springboot/1/springboot3.png)

- 모든 서블릿은 각각 특정 URL에 해당되는 요청을 매핑하는 역할을 수행했다
- 이런 중복 문제를 해결하고자 프론트 컨트롤러 개념을 도입하여 앞단에서 공통 로직을 수행한다
- 많은 스프링 사용자들이 알고있는 ```DispatcherServlet```이 바로 프론트 컨트롤러로 **<u>요청을 앞단에서 먼저 받고 세부 컨트롤러에게 위임하는 역할</u>**을 한다 
- 스프링 부트에서는 ```DispatcherServlet```을 <u>서블릿으로 자동 등록하고, 모든 경로 '/*'에 대해 매핑</u>한다

### 3-3. 스프링 컨테이너

> 프론트 컨트롤러에서 공통 로직을 수행하고 스프링 컨테이너 내부의 빈들이 각각의 로직을 수행한다

![springboot4]({{site.url}}{{site.baseurl}}/assets/images/springboot/1/springboot4.png)

- 프론트 컨트롤러 작업 이후에 ```getBean()```을 통해 Spring Container에 등록된 ```HelloController```를 가져와 사용한다고 가정한다
- 이후 또다른 서블릿이 동일한 빈을 사용한다고 해도 Spring Container는 새로운 ```HelloController```를 만드는 것이 아니라 처음에 만들어둔 ```HelloController```를 전달하는데 이를 **싱글톤 패턴**이라 부른다

## 4. DI

> 스프링의 주요 개념 중 하나인 Dependency Injection에 대해 알아보자

![springboot5]({{site.url}}{{site.baseurl}}/assets/images/springboot/1/springboot5.png)

- 위 그림과 같이 ```HelloController```가 ```SimpleHelloService```의 기능을 사용하는 경우 ```HelloController```가 ```SimpleHelloService```에 의존한다고 말한다
- 추후 새로운 ```HelloService```로 바꿔 사용하고자 한다면, ```HelloController```의 코드를 변경해주어야 하는데 이 경우에 OCP 원칙을 어기게 된다
  - **OCP(개방-폐쇄 원칙)**란 객체 지향 설계에서 가장 중요한 부분으로 <u>확장에는 열려있으나 변경에는 닫혀 있어야함</u>을 의미한다

![springboot6]({{site.url}}{{site.baseurl}}/assets/images/springboot/1/springboot6.png)

- 위 문제를 해결하기 위해 ```HelloService```라는 인터페이스를 만들고 ```HelloController```에서 인터페이스에 의존하도록 설정한다
- ```HelloService``` 관련 클래스들은 모두 ```HelloService```라는 인터페이스를 구현하도록 만든다
- 코드 상으로는 인터페이스를 의존하지만 실제 런타임 시점에는 구현 클래스를 의존해야 한다
- 이처럼 외부에서 실제 구현 클래스를 주입해주는 것을 **의존성 주입**이라고 부르며 ```Assembler```가 이 작업을 수행한다
  - 여기서 ```Assember```가 바로 Spring Container이다
- 의존성 주입에는 생성자 주입, setter 주입 등등 여러가지가 존재하지만 **<u>대부분 생성자 주입을 사용</u>**한다

그렇다면 Spring Container가 생성자 주입을 통해 DI하는 과정을 아래 코드를 통해 살펴보자

``` java
public class HelloController {

    private final HelloService helloService;

    public HelloController(HelloService helloService) {
        this.helloService = helloService;
    }
}
```

- ```HelloController```가 ```HelloService``` 인터페이스를 의존하는 상황으로 가정한다
- Spring Container는 Spring Container에 등록된 빈들 중에 ```HelloService``` 인터페이스를 구현한 타입의 Object를 찾아 의존성 주입을 수행한다

## 5. Spring Bean

### 5-1. 스프링 빈

> 스프링 컨테이너에 의해 관리되는 재사용 가능한 소프트웨어 컴포넌트를 Bean이라고 부른다. 간단히 스프링 컨테이너에 의해 관리되는 자바 객체라고 생각하면 된다

- 과거에는 <u>프로그래머가 직접</u> 자바 객체를 생성하고 다른 클래스에서 해당 객체를 생성하는 방식으로 사용했다. 즉 <u>프로그래머가 객체의 생명주기를 관리</u>했다
- Spring에서는 **IoC(제어의 역전)**라고 하여 개발자가 아닌 **<u>Spring이 제어권을 가지고 객체를 생성하고 관리</u>**한다
- 여기서 Spring이 제어권을 가지는 POJO(Plain Old Java Object) 객체를 **Bean**이라고 한다

### 5-2. 빈을 등록하는 방법

> 스프링 컨테이너에 빈을 등록하는 방법은 크게 수동으로 등록하는 방법과 자동으로 등록하는 방법 2가지가 존재한다

1. **빈 수동 등록하기**

   ``` java
   @Configuration
   public class AppConfig {
       
       @Bean
       public HelloController helloController(HelloService helloService) {
           return new HelloController(helloService);
       }
       
       @Bean
       public HelloService helloService() {
           return new SimpleHelloService();
       }
   }
   ```

   - 메서드 레벨에 ```@Bean```을 붙여주고 클래스 레벨에 ```@Configuration```을 붙여 빈을 수동 등록 가능하다
   - 스프링 컨테이너는 <u>@Configuration이 붙은 클래스를 자동으로 빈으로 등록</u>한 후 해당 클래스를  파싱하여 <u>@Bean이 붙은 메서드를 찾아 메서드 이름으로 빈을 생성</u>해준다
   - ```@Bean```만으로도 빈으로 등록할 수 있지만 <u>싱글톤을 보장받기 위해선 @Configuration을 같이 명시</u>해야 한다
   - **<u>개발자가 직접 제어가 불가능한 외부 라이브러리를 활용하는 경우</u>**에 주로 사용하는 방식으로 Spring이 해당 라이브러리를 싱글톤 방식으로 관리하도록 한다

2. **빈 자동 등록하기**

   - **<u>@Component가 붙은 Object들은 Spring이 컴포넌트 스캔을 통해 빈으로 자동 등록</u>**한다
   - 이 방식 역시 스프링에 의해 싱글톤을 보장받는다
   - **<u>개발자가 직접 만든 클래스를 빈으로 편리하게 등록하고자 하는 경우</u>**에 사용하는 방식이다
   - ```@Controller```, ```@Service```, ```@Repository``` 등의 어노테이션 내부를 살펴보면 ```@Component```가 포함되어 있음을 확인할 수 있다