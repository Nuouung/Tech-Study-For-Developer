# Q. Spring의 핵심 구성요소
<details>
	<summary>Answer</summary>

* IoC/DI, AOP, PSA

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

