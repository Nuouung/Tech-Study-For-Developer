# Q. Spring의 핵심 구성요소
<details>
	<summary>Answer</summary>

* IoC(Inversion of Control)
* DI(Dependency Injection)
* AOP(Aspect-Oriented-Programming)
* PSA(Portable-Service-Abstraction)

* 스프링은 IoC를 통해 객체의 생명 주기가 스프링 컨테이너에 의해 관리되기 때문에 DI와 같은 외부 의존성 주입이 가능하고, 이러한 특징은 객체지향을 살린 자바 애플리케이션을 개발을 가능하게 만들어 준다는 장점을 지닙니다. 

* 또한 AOP를 통해 보안, 트랜잭션, 로깅과 같은 공통 기능을 분리하여 처리할 수 있기 때문에 비즈니스 로직에 집중할 수 있습니다.

* 마지막으로 서비스 추상화를 통해 특정 환경이나 서버, 기술에 종속되지 않으면서 유연한 애플리케이션 개발을 가능하게 만들어줍니다. (PSA)

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [ MangKyu’s Diary](https://mangkyu.tistory.com/156)
* [스프링 스프링이란 무엇인가?](https://12bme.tistory.com/157)
  
## 내용

## 스프링을 사용하는 이유
* 스프링 이전에 엔터프라이즈 자바 어플리케이션 개발을 할 때는 특정 환경에 종속적이고, 비용이 많이들고,  특정 기술에 종속적이었다. 
* 이러한 종속적인 문제는 Java언어를 사용하면서 객체지향의 특징을 활용하지 못했다.
* 이러한 과거의 불편함을 해결하고자 나온것이 Spring
* 이러한 불편함을 해결하는 핵심 기술(?)이 IoC/DI, AOP, PSA이다.

## POJO란
* 자바 오브젝트에 멋진 이름을 붙인것이 전부이다.
* 그렇다고 평범한 자바 오브젝트가 모두 POJO라고 할 수 없다.
* 특정 규약이나 환경에 종속적이지 않고, 객체지향 적인 원리에 충실하게 설계된 자바 오브젝트를 진정한 POJO라고 할 수 있다.
</details>

# Q. Filter vs Interceptor vs AOP의 차이
<details>
	<summary>Answer</summary>

Filter, Interceptor, AOP 모두 공통 기능을 처리하기 위한 방법이지만 적용되는 순서와 범위 사용방법에서 차이를 지닙니다.

Filter는 DispatcherServlet이 호출되기 전, 후로 수행되고 Interceptor는 컨트롤러가 호출되기 전, 후로 처리됩니다. 
필터와 인터셉터는 모두 체인형식으로 처리된다는 특징을 가집니다.

AOP는 공통 관심사를 메서드 단위로 좀 더 세밀하게 적용해줄 수 있습니다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [갓대희의 작은공간 :: Spring Filter, Interceptor, AOP 차이 및 정리](https://goddaehee.tistory.com/154)
* [스프링 MVC 2편 - 백엔드 웹 개발 활용 기술 - 인프런 | 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-2/dashboard)
  
## 내용
### Filter
1. init(): 필터 초기화 메서드
* 서블릿 컨테이너가 생성될 때 호출된다.
2. doFilter()
* 고객의 요청이 올 때 마다 해당 메서드가 호출된다. 필터의 로직을 구현하면 된다. 
3. destroy()
* 필터 종료 메서드, 서블릿 컨테이너가 종료될 때 호출된다. 

### Interceptor

1. preHandle : 컨트롤러 호출 전에 호출된다. 
* preHandle 의 응답값이 true 이면 다음으로 진행하고
* false 이면 더는 진행하지 않는다. 
* false 인 경우 나머지 인터셉터는 물론이고, 핸들러 어댑터도 호출되지 않는다. 

2. postHandle
* 컨트롤러 호출 후에 호출된다. (더 정확히는 핸들러 어댑터 호출 후에 호출.)
* 컨트롤러에서 예외가 발생하면 postHandle 은 호출되지 않는다.


3. afterCompletion
* 뷰가 렌더링 된 이후에 호출된다. 
* afterCompletion 은 항상 호출된다. 
* 예외가 발생한 경우, 예외( ex )를 파라미터로 받아서 어떤 예외가 발생했는지 로그로 출력할 수 있다. 

</details>

# Q. 스프링MVC에서 하나의 요청이들어 왔을 때 처리과정
<details>
	<summary>Answer</summary>
클라이언트가 HTTP요청을 하면 가장먼저 Front Controller의 역할을 하는 DispatcherServlet이  요청을 받아 처리 합니다.

이 후, 요청을 처리할 수 있는 핸들러 어댑터를 조회하여, 컨트롤러를 호출 하게 되고, ModelAndView 객체를 반환 받습니다.

다음으로 ViewResolver를 통해 View에 대한 정보를 받아온 후, Model의 데이터를 렌더링하여 최종 VIew페이지를 반환해주게 됩니다.

만약 컨트롤러에 ResponsBody의 어노테이션이 추가되어있다면, View 페이지가 아닌 Http 메시지 바디에 직접 응답데이터를 출력하여 반환하게 됩니다.
</details>

<details>
	<summary>이해하기</summary>

## Reference
* [스프링 MVC 1편  - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/dashboard)
  
## 내용

</details>

# Q. 빈 생명주기
<details>
	<summary>Answer</summary>

**스프링 빈의 이벤트 라이프 사이클**

`스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백-> 사용 -> 소멸전 콜백-> 스프링 종료`

* 초기화 콜백: 빈이 사용할 수 있는 상태임을 알려줄 수 있다.
* 소멸전 콜백: 안전하게 작업을 종료할 수 있다.

**빈이 생성되고, 소멸되기 직전에 콜백 메소드가 호출된다.**


**빈 스코프**
* 싱글톤: 기본 스코프, 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프
* 프로토타입: 빈의 생성과 의존관계 주입까지만 관여, 더는 관리하지 않는다. (매우 짧은 범위)
* 웹 스코프
	* request: 웹 요청이 들어오고 나갈때 까지 유지된다.
	* session: 웹 세션이 생성되고 종료될 때 까지 유지.
	* application: 웹의 서블릿 컨텍스트와 같은 범위로 유지.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [스프링 MVC 1편  - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/dashboard)
  
</details>

# Q. @Component, @Service, @Controller @Repository 차이점
<details>
	<summary>Answer</summary>

* 스프링은 @Component가 붙은 모든 클래스를 빈으로 등록한다. (스캔 범위 지정 가능.)

* @Controller는 Web MVC에서 사용된다. 클래스 레벨의 @Controller 어노테이션이 존재하는 경우 @RequestMapping을 사용할 수 있다.

* @Service는 내부적으로 @Component를 가지고 있다. 특별한 로직을 수행하지는 않지만 어노테이션을 통해 관점을 분리할 수 있다. (Service는 비즈니스 계층)

* @Repsotiroy는 데이터 접근계층에서 사용되며, 데이터 접근시 발생하는 예외를 스프링 예외로 변환해주는 처리를 해준다.

* @Configuration은 스프링 설정정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 처리한다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [스프링 MVC 1편  - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/dashboard)
* [카카오 면접  @Service,@Controller,@Component 차이](https://baek-kim-dev.site/64)
  
</details>

