### Dependency Injection (DI)

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
  
  https://gmlwjd9405.github.io/2018/11/09/dependency-injection.html
