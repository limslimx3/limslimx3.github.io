---
title: "SpringApplication에 관하여"

toc: true
toc_sticky: true

categories:
  - SpringBoot
tags:
  - SpringBoot
  - inflearn

last_modified_at: 2020-04-14T19:42:00
---
# SpringApplication

## 1. SpringApplication.run()

→ 평소에 Spring Boot를 이용하기 위해서는 @SpringBootApplication을 클래스명 위에 지정해주고 main메서드 안에 SpringApplication.run(클래스명.class, args); 를 적어주면 된다. 하지만 이런 식으로 하게 되면 SpringApplication 이라는 객체의 다양한 메서드를 사용할 수 없고 오직 run() 이라는 메서드만 사용할 수 있게 된다. 이를 해결하기 위해 app 이라는 참조변수를 생성한다. SpringApplication app=new SpringApplication(클래스명.class); 처럼 참조변수를 생성하고 이 참조변수를 통해 SpringApplication 이라는 클래스에 접근한다  

→ 예를 들어 아래의 ApplicationStartingEvent를 SampleListner를 통해 등록한다고 해보자

    import org.springframework.boot.context.event.ApplicationStartingEvent;
    import org.springframework.context.ApplicationListener;
    
    public class SampleListener implements ApplicationListener<ApplicationStartingEvent> {
    
        @Override
        public void onApplicationEvent(ApplicationStartingEvent event) {
            System.out.println("-----------------------");
            System.out.println("Application is starting");
            System.out.println("-----------------------");
        }
    }

이 이벤트는 애플리케이션이 실행되기 전에(정확히 말하면 ApplicationContext 즉, bean을 등록해주기 전에) 발생하는 이벤트이기 때문에 @Component를 붙여 bean으로 등록해준다 하더라도 SpringApplication.run()만으로는 로그가 뜨지 않는다. 하지만 따로 참조변수를 만들어 이를 통해 접근한다면 가능하다. SpringApplication app=new SpringApplication(클래스명.class)으로 인스턴스를 생성하고 app.addListeners(new SampleListeners())를 통해 리스너를 등록하고 app.run(args)를 통해 애플리케이션을 실행시키면 된다. 물론 ApplicationContext에 의해 bean이 등록되고 난 후에 발생하는 이벤트들은 위처럼 listener클래스를 만들고 상속받은 후에 @Component를 통해 bean으로 등록만 해주면 된다  

→ app.setWebApplicationType()의 인자값을 무엇으로 주느냐에 따라 스프링 웹애플리케이션 타입을 바꿀 수 있다(Servlet, Reactive, None 3가지 종류가 있다)
