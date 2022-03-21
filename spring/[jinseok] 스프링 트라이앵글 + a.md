## Spring Container

* 스프링 프레임워크의 핵심 컴포넌트(구성요소)
* 애플리케이션을 구성하는 빈을 생성하고 관리하는 컨테이너이다.
* Bean Factory와 이를 상속한 ApplicationContext 2가지의 유형이 존재

#### Bean Factory

* 스프링 설정파일에 등록된 빈 객체를 생성하고 관리하는 기본적인 기능만을 제공
* 컨테이너가 생성될 때 빈을 생성하지 않고 클라이언트의 요청이 있을 때 빈을 생성하는 Lazy Loading을 사용
* 일반적으로 스프링 프로젝트에서 사용되는 ApplicationContext가 BeanFactory를 상속하기 때문에 직접적으로 Bean Factory를 사용할 일은 많지 않다!

#### Application Context

* Bean Factory와 마찬가지로 빈 객체를 생성하고 관리하는 기능을 가짐
* Bean Factory가 빈을 생성하고 관리하는 기본적인 기능만을 제공하는 것과는 달리 ApplicationContext는 애플리케이션 내에서 트랜잭션 관리, 메시지 기반의 다국어 처리, AOP 처리 등 많은 기능을 제공
* 스프링 프로젝트가 실행되며 컨테이너가 구동될 때 객체를 생성하는 Pre-Loading 방식
* 여러 종류의 ApplicationContext 구현체가 있지만 웹 기반의 스프링 애플리케이션을 개발하면 XmlWebApplicationContext가 주로 사용됨

## Spring Bean

* 스프링 빈은 스프링 컨테이너에 의해 관리되는 자바 객체를 의미함 (자바 진영은 커피를 참 좋아하는 것 같다)
* 컨테이너가 객체를 관리하기 때문에 IoC와 많은 연관이 있음.
* 스프링 프레임워크에서 스프링 빈을 얻기 위해 ApplicationContext.getBean() 과 같은 메소드를 사용할 수 있음

## Dependency Injection (DI)

* 한국어로는 의존성 주입 혹은 의존관계 주입
* 객체의 의존성이 객체 자체가 아니라 프레임워크에 의해 주입되는 설계 패턴
* 객체의 의존성이 프레임워크에 의해 동적으로 주입되므로 주입이 변경되더라도 그 구현 자체를 수정하지 않아도 됨
* 의존성 주입은 IoC의 형태 중 하나이다. (IoC <- 제어의 역전 : 프레임워크가 애플리케이션을 제어한다!)
* 의존성 주입의 의도는 객체 생성과 사용의 관심을 분리하는 것. 이를 통해 코드의 가독성과 재사용성이 높아진다.

#### 스프링 프레임워크에서의 DI 방법

* Constructor Injection: 생성자를 통해 의존성을 주입하는 방법

예를 들어 MemberService라는 이름의 객체가 있다면

````
private final [주입받고자 하는 객체] target;

@Autowired
public MemberService([주입받고자 하는 객체] target) {
  this.target = target;
}
````
(생성자가 하나라면 @Autowired는 생략 가능)

* Method(Setter) Injection: 세터메소드(수정자)를 통해 의존성을 주입하는 방법

````
private final [주입받고자 하는 객체] target;

@Autowired
public void setTarget([주입받고자 하는 객체] target) {
  this.target = target;
}
````

* Field Injection: 필드 주입

````
@Autowired private final [주입받고자 하는 객체] target;
````

#### DI의 장점

* 종속성이 감소한다. : 특정 객체가 구체적인 구현체를 바라보지 않아도 되기 때문에 코드간의 종속성이 줄어든다. (DI가 없다면 반드시 코드상에 구현체를 작성해야 하기 때문 ex. List<Integer> list = new ArrayList<>();)
* 재사용성이 증가한다. : 특정 인터페이스의 다른 구현이 필요할 경우, 그 인터페이스를 바라보는 모든 코드의 수정 없이 해당 구현을 사용할 수 있다.
* 더 많은 테스트 코드를 만들 수 있다. : 테스트를 수행할 때 자유롭게 Mock 객체를 사용할 수 있다.
* 가독성이 증가한다. : 코드가 특정 구현체를 바라보지 않고 보다 추상적인 '역할'을 바라보므로 코드의 가독성이 높아진다. (ex. DI가 없는 경우 memoryMemberServiceImpl.getMember() / DI가 있는 경우 memberService.getMember() 훨씬 읽기 쉽다.)
* 구현과 설계가 분리되므로 거기에서 발생되는 가독성의 증가도 있다. (객체의 주입을 조정하는 Configuration 파일과 구현 파일을 분리할 수 있게 됨!)
  

## IoC(Inversion of Control)
  
## POJO (Plain Old Java Object)

"스프링의 본질은 엔터프라이즈 서비스 기능을 POJO에 제공하는 것이다." - Professional Spring Framework, 2005
  
* POJO란 객체 지향 원리에 충실하면서 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트를 말함
* 2000년대 초반 EJB의 한계에 반발하며 일어난 운동으로 마틴 파울러(Martin Fowler)가 그의 컨퍼런스를 준비하다 탄생한 용어라고 함
  
#### EJB(Enterprise Java Bean)

* 2000년대 초반 웹 개발을 위한 자바 표준기술
* 인스턴스 풀링, 설정에 의한 프랜젝션 처리 등 다양한 기능을 제공했지만 프레임워크의 복잡성과 객체지향적이지 않은 성격 때문에 많은 개발자들에 의해 외면, 이후 POJO를 통한 스프링의 탄생에 영향을 주었다
  
#### POJO의 조건

1. 특정 규약에 종속되지 않는다. (자바언어와 꼭 필요한 API 외에는 종속되지 않아야 한다.)
2. 특정 환경에 종속되지 않는다. (특정 기업의 프레임워크 혹은 서버에서만 동작한다면 POJO라 할 수 없다.)
3. 객체지향적 원리에 충실해야 한다. (POJO는 객체지향적인 자바 언어의 기본에 충실해야 한다. 자바 언어로 작성되었다 하더라고 책임과 역할이 서로 다른 코드를 특정 클래스에 몰아 넣는 코드는 POJO가 아니다.)
  
#### POJO의 장점
 
* 깔끔한 코드
* 간편한 테스트
* 객체 지향적 설계를 자유롭게 적용할 수 있음
  
#### 대표적인 POJO 프레임워크
  
* 스프링 프레임워크
* 하이버네이트 (JPA)
  
