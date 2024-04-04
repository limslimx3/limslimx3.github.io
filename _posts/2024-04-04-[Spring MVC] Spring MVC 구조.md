---
title: "[Spring MVC] Spring MVC 구조"

toc: true
toc_sticky: true

categories:
   - Spring
tags:
   - Spring
   - MVC

last_modified_at: 2024-04-04T23:00:00


---

# Spring MVC 구조 및 흐름

> 전체적인 Spring MVC 구조와 동작 흐름에 대해 알아보자

## 배경지식

> 간단히 Spring MVC가 무엇인지 살펴보자

### MVC 패턴?

- 애플리케이션 개발 시에 사용하는 디자인 패턴
- 애플리케이션 개발 영역을 Model, View, Controller로 나눠 각 역할에 따른 코드를 분리한다
  - Controller는 Client의 요청을 직접 전달받는 엔드포인트로 Model과 View를 연결해준다
  - View는 Model을 이용하여 Client가 보는 화면에 각종 Resource를 보여주는 역할을 수행한다
  - Model은 비즈니스 로직 처리결과 등의 데이터를 담아 View에게 전달하는 역할이다
- 하나의 파일에 모든 코드를 집어넣었던 것과 비교하면 유지보수성 측면에서 확실한 이점이 존재한다



## Spring MVC 구조 및 흐름

> 우선 Spring MVC의 주요 요소들에 대해 간단히 용어정리해본 후 전체적인 처리 흐름에 대해 살펴보자

![login1]({{site.url}}{{site.baseurl}}/assets/images/springmvc/mvc1.png)

### DispatcherServlet

- Spring MVC의 핵심으로 **프론트 컨트롤러**의 역할을 수행한다
  - 여기서 프론트 컨트롤러란 여러 컨트롤러가 가지는 공통기능들을 추출하여 사전에 한번에 처리하는 패턴이다
- ```HandlerMapping```, ```HandlerAdapter```, ```ViewResolver``` 등 여러 요소들을 필요에 맞게 사용할 수 있도록 도와준다
- 프론트 컨트롤러로서 들어오는 **<u>모든 HTTP 요청을 처리하고 적절한 핸들러에 해당 요청을 전달하고 응답을 생성하는 역할</u>**을 수행한다

### HandlerMapping

- 들어오는 **<u>HTTP 요청을 적절한 핸들러에 매핑</u>**하는 기능을 수행한다
- 요청의 URL, Http Method, Http Header 등의 정보를 기반으로 어떤 핸들러가 이를 처리할지 결정한다

### HandlerAdapter

- ```DispatcherServlet```과 ```Handler```의 사이에 위치하며 상호작용을 돕는다
- ```HandlerMapping```에 의해 요청을 처리할 핸들러를 ```DispatcherServlet```으로부터 전달받아 ```HandlerAdapter```가 **<u>해당 핸들러를 실행</u>**시킨다
- 핸들러 수행결과 반환값을 ```ModelAndView```로 담아 ```DispatcherServlet```에게 전달한다

### Handler

- 특정 **<u>Http 요청에 해당되는 주요 비즈니스 로직을 처리</u>**하는 부분이다
- 다른 이름으로 ```Controller```라고도 부른다

### ViewResolver

- 핸들러에서 반환된 뷰 이름을 실제 뷰 템플릿으로 매핑하는 역할을 수행한다
  - 즉, ```View```를 반환한다
- ```JSP```, ```Thymeleaf``` 등 다양한 뷰 템플릿 기술을 지원한다

### View

- 뷰 템플릿을 의미하며 실제로 Client에게 응답을 렌더링한다

