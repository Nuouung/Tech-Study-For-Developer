## 1. IoC(Inversion of Control)
Ioc : 제어의 역전이라는 말로 개발자가 아닌 툴(스프링)이 제어권을 가져 클래스가 의존 객체를 직접 만드는 것들이 아니라 주입받아서 사용하는것을 말한다.
IoC 컨테이너는 빈 설정 소스로부터 빈 정의를 읽어들이고, 의존관계를 설정하여 빈을 구성하고 제공해주는데 기본적으로 **빈을 싱글톤으로 제공**해주기때문에 제공된 빈은 항상 같은 객체일 것이며 인스턴스가 과다하게 생성되어 서버에 부담을 주는 일을 막을 수 있다.

## 2. DI(Dependency Injection)
DI : 의존성 주입, 각 클래스간의 의존관계를 빈 걸정 정보를 바탕으로 컨테이너가 자동으로 연결하는 것으로 객체들 간의 의존성을 줄이기 위해 사용되는 스프링의 IOC 컨테이너의 구체적 구현 방식을 말한다.
```java
class Coffee {...} // interface로 설계할 수도 있다

// Coffee 클래스를 상속
class Cappuccino extends Coffee {...}
class Americano extends Coffee {...}

// Programmer.java
class Programmer {
    private Coffee coffee;

    public Programmer() {
    	this.coffee = new Cappuccino(); // 직접 수정
        // 또는 
        this.coffee = new Americano(); // 직접 수정
    }
}
```
이렇게 코드를 작성한다면 Americano나 Cappuccino코드를 수정한다면 일일히 다 찾아서 수정해야함
```java
class Programmer {
    private Coffee coffee;

    // 그 날 마실 커피를 고를 수 있게된 개발자
    public Programmer(Coffee coffee) {
    	this.coffee = coffee;
    }
    
    public startProgramming() {
    	this.coffee.drink();
        ...
    }
}
```
이렇게 DI를 이용한다면 해당 클래스(Americano나 Cappuccino)만 수정하면 됨

### 장점
    1. 코드의 재활용성을 높여준다.
    2. 객체 간의 의존성(종속성)을 줄이거나 없엘 수 있다.
    3. 객체 간의 결합도이 낮추면서 유연한 코드를 작성할 수 있다.

### 방법
Spring은 @Autowired 애노테이션을 이용한 다양한 의존성 주입 방법을 제공한다.
@Autowired 애노테이션은 Spring에게 의존성을 주입하라는 지시자 역할로 쓰이는데 생성자, 필드, 세터에 붙일 수 있다.

## 3. AOP(Aspect Oriented Programming)
AOP : 관점 지향 프로그래밍, 여러 개의 핵심 비즈니스 로직 외에 공통으로 처리되어야 하는 로그 출력, 보안처리, 예외 처리와 같은 코드를 모아서 처리를 편리하게 해주는 프로그래민 기법

Aspect : 소스 코드상에서 다른 부분에 계속 반복해서 쓰는 코드들을 모듈화 한 것.
Target : Aspect를 적용하는 곳 (클래스, 메서드 .. )
Advice : 실질적으로 어떤 일을 해야할 지에 대한 것
JointPoint : Advice가 적용될 위치
PointCut : Jointpoint 의 부분 집합으로 실제로 Advice가 적용되는 Jointpoint 를 나타냄

## 5. POJO(Plain Old Java Object)
POJO : 

## 5. PSA(Portable Service Abstraction)
