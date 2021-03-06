# Q. Java언어의 장점 및 동작과정
<details>
	<summary>Answer</summary>

### 장점

* JVM위에서 실행되기 때문에 OS에 독립적이다.
* GC(Garbage Collector)가 존재하기 때문에, 메모리 관리를 직접하지 않아도 된다.

### 동작과정

1. Java Application은 클래스 로더에 의해 JVM 내의 Runtime Data Area에 적재된다.
2. 이 후, Excution Engine에 의해 명령어 단위로 실행된다.

![helloworld-1230-1](https://user-images.githubusercontent.com/26343023/154325128-254b9636-2ef5-47d2-ae94-3500d125f76b.png)

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [NAVER D2](https://d2.naver.com/helloworld/1230)
* [JAVA JVM 동작원리 및 기본개념](https://steady-snail.tistory.com/67)
* [#자바가상머신, JVM(Java Virtual Machine)이란 무엇인가?](https://asfirstalways.tistory.com/158)  
* [How JVM Works - JVM Architecture? - GeeksforGeeks](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/)
* [class loader image 출처](https://m.blog.daum.net/sincere520/50)


## 내용

* 자바 바이트코드는 `JRE위에서 동작` 한다.
* JVM은 JRE의 요소 중 하나로써 자바 어플리케이션을 `클래스 로더`를 통해 읽어 들여 자바 API와 함께 실행하는 역할을 수행.
![jre](https://user-images.githubusercontent.com/26343023/154325177-a391975f-de96-4799-8443-b7752075d81b.png)

### 1. 클래스 로더

* 클래스 로더는 컴파일 타임이 아니라, 런타임 중 클래스를 처음 참조할 때 해당 클래스를 로드 & 링크한다.
	* 클래스 로더는 로딩 -> 링킹 -> 초기화의 과정을 거친다.
		* 링킹은 올바른 코드인지 확인해서(검증), 필요한 메모리를 할당하고(준비), 상수 풀의 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경한다. (분석)
		* 마지막으로 클래스 변수의 값을 초기화 한다.
			* 즉, static initializer를 수행 및 필드의 값을 초기화 한다.

![image](https://user-images.githubusercontent.com/26343023/154325867-3ec6616d-379d-4f52-a54a-fc19ef7fe6c5.png)
  
### 2. 런타임 데이터 영역
* Runtime Data Area는 운영체제가 JVM에게 할당받는 메모리 영역
	* 메모리 공간을 6개의 영역으로 나누어서 사용한다.

![helloworld-1230-4](https://user-images.githubusercontent.com/26343023/154325214-ef89e5bd-95a1-43dd-a556-898d73547494.png)
  
#### PC Register

* 현재 수행 중인 JVM 명령의 주소를 가지고 있다.

#### JVM Stack
* 스택 프레임(Stack Frame)구조체를 저장하게 된다.
* 메서드가 수행별로 스택프레임이 생성되고, 메서드 종료시 반환된다.
* 각 스택 프레임에는 지역 변수,  파라미터 값, 메서드가 속한 클래스의 런타임 상수 풀에 대한 레퍼런스 값 등을 쌓게된다.
* 컴파일 타임에 결정되기 때문에, 스택 프레임의 크기도 메서드에 따라 크기가 고정된다.

#### Native Method Stack
* 이 메모리 공간은 자바 이외의 코드를 위한 공간이다.
* JNI(Java Native Interface)를 통해 호출하는 C/C++ 등의 코드를 수행하기 위한 스택.

> 위 3개의 메모리 영역은, 쓰레드 단위로 생성이 된다.
> 즉 쓰레드 별로 독립적인 메모리 공간을 가지고 프로그램이 처리된다.
> 
> 반면에, 아직 설명하지 않은 Heap과 Method Area는 모든 쓰레드에서 공유할 수 있다.
> 따라서 멀티쓰레드 환경에서 동시성에 대한 문제가 발생할 수 있다.

#### Heap
* 인스턴스나 객체를 저장하는 공간이다.
* 쉽게 new 연산자로 생성 된 인스턴스는 동적으로 Heap메모리에 할당된다.
* Heap 영역은, GC의 대상이되는 공간으로써, JVM 성능에 가장 많은 영향을 끼치게되는 공간이다.

#### Method Area
* 메서드 영역은 모든 스레드가 공유하는 영역으로 JVM이 시작될 때 생성된다.
* JVM이 읽어 들인 모든 바이트코드를 보관한다.

#### Runtime Constant Pool
* 메서드 영역에 포함 된 공간이다. 
* JVM동작에 가장 핵심적인 역할을 수행하는 곳이다.
* 각 클래스와 인터페이스의 상수뿐 아니라, 메서드와 필드에 대한 모든 레퍼런스까지 담고 있는 테이블이다.
* 어떤 메서드나 필드를 참조할 때 JVM은 Runtime Constant Pool을 통해 실제 메모리상 주소를 찾아서 참조한다.

### 3. 실행 엔진(Execution Engine)
클래스 로더를 통해 JVM의 런타임 데이터 영역에 배치된 바이트코드는 실행 엔진에 의해 실행된다.

* 실행 엔진은 바이트코드를 명령어 단위로 읽어서 실행한다.
	* CPU가 기계 명령어를 하나씩 실행하는 것과 비슷한다.
* 실행 엔진은 바이트코드를 기계가 수행할 수 있는 코드로 명령어 단위로 해석하면서 실행하게 된다.
	* 이를 인터프리터 방식이라 한다.
* 인터 프리터 방식은 [해석 -> 실행]의 과정을 거치기 때문에, 전체적인 실행시간이 느리다는 단점을 가지고 있다.
* 이러한 단점을 보완하고자, JVM은 내부적으로 해당 메서드가 얼마나 자주 수행되는지 체크하고, 일정 수준을 넘어가면 전체를 컴파일하여 네이티브 코드로 변경해서, 변경된 코드를 캐시를 통해 빠르게 수행할 수 있도록 한다.
	* 이러한 실행방식은 JIT(Just-In-Time)컴파일러를 사용한다.
 
</details>


# Q. String, String Buffer, StringBuilder
<details>
	<summary>Answer</summary>

String은 불변 객체이며, String Buffer는 멀티 스레드 환경에서 thread-safe하게 사용할 수 있는 특징을 가지며, String Builder는 단일 스레드 환경에서 가장 좋은 성능으로 처리될 수 있다는 특징을 가지고 있습니다.

</details>

<details>
	<summary>이해하기</summary>

## Reference

  
## 내용

### 불변 객체
* 불변객체란, 생성 후 상태를 바꿀 수 없는 객체를 의미.

#### 장점
* 객체를 Thread-Safe하게 사용할 수 있다.

#### 단점
* 메모리 공간을 많이 사용하게 된다. 문자열의 변경은, 새로운 문자열의 할당을 의미한다.


### Thread-Safe
* 멀티 스레드 환경에서, 동시에 하나의 자원을 다룰 때 순서를 제어하여 데이터의 무결성을 보장할 수 있도록 해주는 것.
* 세마포어나 뮤텍스와 같은 도구를 사용하여 공유자원에 대한 접근을 동기화 한다.
* 따라서, 추가적인 연산이 수행된다.


</details>

# Q. 객체지향의 특징
<details>
	<summary>Answer</summary>

* 추상화
	* 인터페이스와 구현을 분리하여, 필수 속성만으로 객체를 묘사한다.

* 캡슐화
	* 캡슐화란 속성과 함수를 하나로 묶는 것.
	* 객체의 세부 내용이 외부에 드러나지 않아, 변경에 대한 파급효과가 적다.
	* 캡슐화를 통해 재사용성을 높일 수 있다.
	* 인터페이스가 단순해지고, 객체 간 결합도가 낮아진다.

* 다형성
	* 같은 요청에 대해 다양한 방법으로 응답할 수 있다는 것을 의미한다.
	* 오버로딩을 통해 같은 이름의 함수지만 다른 인자값을 받아 처리할 수 있다.
	* 오버라이딩을 통해 새롭게 정의된 기능이 수행되도록 할 수 있다.

* 상속
	* 상속을 통해 기존 클래스를 수정하지 않고, 확장하여 사용할 수 있다.
	* 클래스의 재사용성을 높여준다. 
 
* 정보 은닉
	* private
	* 다른 객체에 자신의 정보를 숨기고, 객체 자체에서만 사용할 수 있도록한다.
	* 정보은닉을 통해 불필요한 접근을 차단하여, Side Effect를 최소화 할 수 있다.
	* 유지보수와 소프트웨어 확장 시 오류를 최소화할 수 있다.

* 캡슐화 vs 은닉화 차이
	* 캡슐화는 속성과 함수를 묶는 것, 캡슐화를 통해 추상화 및 재사용에 대한 단위가 된다.
	* 정보은닉은 캡슐화를 통해 실현된다.
	* 은닉화는 캡슐의 내부와 외부를 구별짓는 장치가 된다.


</details>

<details>
	<summary>이해하기</summary>

## Reference
* [객체지향 프로그래밍(OOP)의 특징(4)과 설계 원칙(5) — 팽이돌리기](https://gre-eny.tistory.com/269)
* [캡슐화와 정보은닉](https://frontierdev.tistory.com/93)

  
## 내용

### 객체지향 이란 ?
* 컴퓨터 프로그램을 명령어의 목록으로 보는것이 아니라, 여러 개의 독립된 단위들의 모임으로 파악하고자 하는 것. 
* 각각의 객체는 메시징을 통해 커뮤니케이션할 수 있다.


</details>

# Q. OOP의 설계원칙(SOLID)

<details>
	<summary>Answer</summary>

### SRP: 단일 책임 원칙(single responsibility principle)
* 하나의 클래스는 하나의 책임만 가지도록 한다.
* 책임이라는 것은 모호한 개념이다. 중요한 기준은 변경이다.
* 변경이 있을 때 파급 효과가 적다면 단일 책임 원칙을 잘 따른 것.


### OCP: 개방-폐쇄 원칙 (Open/closed principle) 
* 가장 중요
* 확장에는 열려있지만, 변경에는 닫혀있어야 한다.
* 다형성을 활용해 지킬 수 있다.
* 즉, interface를 통해 무한한 확장을 할 수 있지만, 기존 코드는 변경하지 않도록 할 수 있다.

### LSP: 리스코프 치환 원칙 (Liskov substitution principle) 
* 프로그램의 객체는 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀수 있어야 한다.
* interface를 구현한 클래스에서는, 반드시 모든 메서드를 오버라이딩 해야한다. 이를 통해 신뢰성을 높일 수 있다.
* 또한, 만약 go라는 메서드에서 후진을 하도록 구현하면 안된다. 즉, 올바르게 구현해야 한다. 
	* go메서드에서 후진(back)의 기능을 구현했다면 LSP 위반이다.
	* 느리더라도 앞으로 가야한다.

### ISP: 인터페이스 분리 원칙 (Interface segregation principle) 
* 범용 인터페이스하나보다, 명확한 여러개의 인터페이스를 사용하도록 분리하는 것이 좋다.
* 인터페이스가 명확해지며, 대체 가능성이 높아진다.


### DIP: 의존관계 역전 원칙 (Dependency inversion principle)
* 추상화에 의존해야지, 구체화에 의존하면 안된다.
* 의존이란, 코드를 알고있다는 것. 클라이언트 코드가 interface만 바라보도록 한다.
* 역할에 의존해야지, 구현에 의존해서는 안된다 !

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [스프링 핵심 원리 - 기본편 - 인프런 | 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
  
## 내용

* 저 정도로는 답변해야 하지 않을까 ?

</details>

# Q. 클래스, 객체, 인스턴스 차이

<details>
	<summary>Answer</summary>

* 클래스는 붕어빵 틀, 객체는 붕어빵, 인스턴스는 틀로 찍어낸 각각의 붕어빵.
* 클래스는 설계도, 틀을 의미한다.
* 객체는 소프트웨어 세계에 구현할 대상. `클래스의 인스턴스` 라고도 부른다.
	* 객체는 모든 인스턴스를 대표하는 포괄적 의미를 가진다.
* 인스턴스는 `실제 구현된 구체적 실체`이다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [자바, Java 클래스(class), 객체(object), 인스턴스(instance) 차이](https://computer-science-student.tistory.com/319)
  

</details>

# Q. Garbage Collection 에 대해 설명해 주세요
<details>
	<summary>Answer</summary>

* Java에서 Garbage Collectior이란 동적 메모리 관리를 처리 해주는 하나의 쓰레드를 의미합니다.
* 따라서, GC이 동작할 때는 stop-the-world가 발생하고, 이는 나머지 작업들이 멈추게 되는 현상을 의미합니다.
* Garbage Collection은 지속적인 튜닝과 모니터링을 통해 해당 서비스에 가장 적합한 값을 찾는다면, 어플리케이션의 성능을 높일 수 있습니다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [NAVER D2](https://d2.naver.com/helloworld/1329)
* [tech-refrigerator/Garbage Collection.md at master · GimunLee/tech-refrigerator · GitHub](https://github.com/GimunLee/tech-refrigerator/blob/master/Language/JAVA/Garbage%20Collection.md#garbage-collection)
  
## 내용

### Garbage Collection 의 처리 대상
	1. 객체가 Null일 때
	2. 블록이 종료었을 때, 블록안에서 생성된 객체
	3. 부모 객체가 Null일 때, 포함관계의 자식 객체

### Garbage Collection의 메모리 해제 과정

> Marking -> Normal Deletion -> Compacting의 과정을 거친다.

#### Marking
* 모든 오브젝트를 스캔해서, GC메모리가 사용되는지 확인한다.

#### Normal Deletion
* 참조되지 않는 객체를 제거하고, 메모리를 반환
* 반환되어 비어진 블록의 위치는 Allocator가 저장해 두었다가, 새로운 오브젝트가 선언되면 할당한다.

#### Compacting
* 성능 향상을 위해, 참조되지 않는 객체를 제거한 후, 남은 객체를 압축하여 메모리 공간을 확보한다.

### Generation Garbage Collection

> Mark & Compact 방식은 비효율 적이다.
> 프로그램은 대체로 처음에 많은 공간을 사용하고, 시간이 지날수록 적은 객체만 사용한다.

<img width="350" alt="java-gc-004" src="https://user-images.githubusercontent.com/26343023/154737452-2489a911-cff4-4ee4-97cd-117c92530fdb.png">

* 이러한 현상을 멋지게 `Weak Generational Hypothesis` 라고 한다.
* `Weak Generational Hypothesis` 는 새롭게 만든 객체는 금방 사용하지 않는 상태가되고, 오래살아남은 객체는 신규객체를 참조하는 경우가 매우 드물다는 가설이다.
* 이 가설에 기반해 자바는 Young영역과 Old영역으로 메모리를 분할하고, 신규 생성 객체는 Young, 오래 살아남은 객체는 Old에 구분하여 보관한다.
* Young영역에서의 GC발생을 MinorGC
* Old 영역에서의 GC 발생을 Major GC(혹은 Full GC)라고 한다.


> 핵심은, 메모리 공간을 나누어서 Marking의 범위를 최소화 하는 것 같다…

<img width="350" alt="java-gc-006" src="https://user-images.githubusercontent.com/26343023/154737464-7b258467-b4f4-48d0-9b42-1b730a386ee5.png">
	
* Eden Space가 차기전에는 GC가 발생하지 않는다.
* Eden Space가 가득차면 GC가 발생하고, 살아남은 객체는 S0으로 이동. 비 참조 객체는 clear !
* 이런식으로 공간을 나누고, 살아남는 객체는 S0, S1에 관리한다.
* Survivor Space에 오래살아남는 객체는 MinorGC가 발생할 때마다 Aged(나이를 증가) 시키며 관리한다.
* 객체의 나이가 기준을 넘어서게 될 때, Old Generation으로 이동된다.
* 프로그램이 동작하면서, Young영역이 부족해 진다면, 결국 Marking의 범위는 OldGeneration까지 확장되어 당연히 Stop-the-world가 오래 발생하게 된다.


</details>

# Java는 Call By Reference 인가 Call By Value 인가?
<details>
	<summary>Answer</summary>

* Call By Value
* 값을 복사해서 던진다. 따라서 전달받은 값을 변경해도 원본은 변경되지 않는다.
* 참조 변수의 경우에는 주소값을 복사해서 던진다.
	* 따라서 외부에서 값을 변경할 수 있다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [Java Java는 Call by reference가 없다](https://deveric.tistory.com/92) 

</details>

# Q. 예외처리(CheckedException , UnCheckedException)
<details>
	<summary>Answer</summary>

![2019-03-02-java-checked-unchecked-exceptions-1](https://user-images.githubusercontent.com/26343023/154745663-6e74bfeb-4b33-4571-8606-5866b9b6e14b.png)

	
* Checked Exception
	* RuntimeExcetipn을 상속하지 않는 클래스


* UnChecked Exception
	* Error와 RuntimeException을 상속한 예외 클래스를 의미

![2019-03-02-java-checked-unchecked-exceptions-2](https://user-images.githubusercontent.com/26343023/154745652-8168b724-1164-4311-9f1b-c39ae5ea65a8.png)

</details>

<details>
	<summary>이해하기</summary>

## Reference
[자바 예외 구분: Checked Exception, Unchecked Exception](https://madplay.github.io/post/java-checked-unchecked-exceptions)
  
## 내용

### Error
* 비정상적인 상황이 발생한 경우, 주로 JVM에서 발생 한다.
* Error는 애플리케이션 코드에서 잡으면 안된다. 
	* Error = 잘못된 사용 혹은 문제를 의미
* OutOfMemoryError, ThreadDeath, StackOverflowError등이 존재한다.

### Exception
* 정상적인 흐름을 벗어나는 경우, 개발자가 상황을 예측하고 핸들링할 수 있다.

</details>


# Q. interface와 abstract class차이
<details>
	<summary>Answer</summary>
	
기본적으로 클래스와 인터페이스의 차이점을 지니고 있습니다. 
인터페이스는 다중 구현이 가능하며, public final의 멤버만 지닐 수 있는 반면 추상 클래스는 단일 상속만 가능하며, private, protected와 같은 클래스 멤버를 가질 수 있습니다.

만약 여러개의 자식클래스에서 공통으로 처리되는 코드가 존재한다면 추상클래스로 정의하여, 공통부분은 공유하고, 부분적인 확장을 해 나가는 것이 더 효율적입니다.
반면 인터페이스는 완전한 추상화가 필요한 경우 사용되며, 구현체가 아닌 동작에 대한 정의만 필요한 경우 사용할 때 적절합니다.

</details>

<details>
	<summary>예시</summary>

- 니트와 면티는 모두 상의에 속한다.
- 니트와 면티는 모두 `입는다()` 와 `세탁한다()`의 기능을 수행할 수 있다.
- `입는다()`는 니트든 면티든 그냥 입으면 된다. (공유해서 쓰면 된다.)
- 면티는 세탁이 가능하지만, 니트는 손빨래를 해야 한다. (각자 재정의해서 쓰면 된다.)
- 이 때 상의라는 상위그룹의 개념은 abstract class로 정의하는것이 더 깔끔하다.
	
``` java
abstract class 상의 {
 
    // Non-abstract methods
    // Having as default implementation
    public void 입는다() {
        System.out.println("상의를 입는다");
    }
 
    // Method 2
    // Abstract methods which will be
    abstract public void 세탁한다();
}
```
- 만약 빨래방에서 사용하는 상의 객체를 정의한다면 ??
- 빨래방에서는 옷을 입을 필요가 없다. 즉, `입는다()`라는 공통의 처리가 불필요하다.
- 그냥 interface로 정의하는게 더 깔끔하다.

``` java
// Interface
interface 상의 {
    // Abstract method
    void 세탁한다();
}
```
</details>

<details>
	<summary>이해하기</summary>

## Reference
- [JAVA 추상클래스 VS 인터페이스 왜 사용할까? 차이점, 예제로 확인 :: 마이자몽](https://myjamong.tistory.com/150)
- [abstract class vs interface](https://www.geeksforgeeks.org/difference-between-abstract-class-and-interface-in-java/)
- [interface 특징](https://limkydev.tistory.com/197)
- [abstract](https://www.geeksforgeeks.org/abstract-classes-in-java/)


## 내용

### 먼저 고민해보기
* [링크](https://www.geeksforgeeks.org/java-gq/abstract-class-and-interface-in-java-gq/)

### abstract class
	
* 추상클래스는 IS -A “~이다”
* 추상 클래스는 생성자를 정의할 수 있지만 인스턴스를 생성할 수 없다.
* 추상 클래스의 생성자는 클래스에 필요한 제약을 줄 때 사용한다. - [참조](https://hashcode.co.kr/questions/298/%EC%B6%94%EC%83%81%ED%81%B4%EB%9E%98%EC%8A%A4%EB%8F%84-%EC%83%9D%EC%84%B1%EC%9E%90%EB%A5%BC-%EA%B0%80%EC%A7%88%EC%88%98-%EC%9E%88%EB%82%98%EC%9A%94)
* 추상 클래스는 static 메서드를 정의할 수 있다.

### interface

* 인터페이스는 HAS -A “_ 을 할 수 있는”
* 확장의 의미를 가진다.
* ~able
* 인터페이스는 다중 구현이 가능하다.
* 인터페이스는 상수, 추상메소드, 디폴트메소드, 정적메소드를 정의할 수 있다. (디폴트, 정적 메소드는 java8 추가)
	* 상수란 멤버 변수(public final static)를 의미한다. 변경할 수 없고, 참조만 가능. (절대적)
	* 정적메소드 또한 static 키워드를 사용했기 때문에 참조만 가능. (절대적)
	* default 메소드는 선택적으로 사용 가능. (선택적)
	* 추상메소드는 반드시 오버라이딩해서 사용해야 함.(강제적)
	
</details>

# Q. 자바 1.8 버전에서 새롭게 추가된 주요 Feature에 대해 설명해 주세요
<details>
	<summary>Answer</summary>

대표적으로 람다와 스트림, Optional, java.time패키지가 추가되었습니다.

스트림 API를 사용하여 데이터에 대한 접근을 공통으로 처리할 수 있고, 람다식을 사용해 함수형 프로그래밍이 가능해져 코드의 재사용성을 높이고, 가독성을 높일 수 있게 되었습니다.

또한 기존의 Calendar클래스의 단점을 보완한 java.time패키지를 통해 날짜 및 시간에 대한 처리를 더욱 손쉽게 사용할 수 있게되었습니다.
	
Optional은 NPE(NullPointerException)을 회피하기 위한 일종의 Wrapper클래스로써, 복잡한 조건문 없이 null값으로 인한 예외를 처리할 수 있습니다.


</details>

<details>
	<summary>이해하기</summary>

## Reference
* [코딩의 시작, TCP School](http://www.tcpschool.com/java/java_intro_java8)
* [Optional](http://www.tcpschool.com/java/java_stream_optional)
* [Optional 올바르게 사용하기](https://www.latera.kr/blog/2019-07-02-effective-optional/)
* [Optional 장단점](https://maivve.tistory.com/332)
  
## 내용

### 1. 람다 표현식(Lamda Expression)
* 익명 함수라고도 부르며, 메소드를 하나의 식으로 표현한 것을 의미.
* 함수형 프로그래밍이 가능하게 되었고, 그로인해코드의 가독성을 높일 수 있게  되었다는 것이 가장 큰 장점.

### 2. 스트림 API
* 데이터를 추상화 하여 다루어, 배열이나 컬렉션뿐 아니라 파일에 저장된 데이터 또한 같은 방법으로 다룰 수 있게 해주는 API (with 람다)
	* 스트림API 이전에 Java에서는 배열, 컬렉션을 이용해 데이터를 저장했다.
	* 배열, 컬렉션을 다룰 때문제점은 코드의 가독성이 떨어지고, 재사용이 거의 불가능하다는 것.
	* 또한 데이터베이스 쿼리와 같이 정형화된 처리 패턴을 가지지 못했기 때문에 데이터마다 다른 방법으로 접근해야 했다.
		* 이건 무슨말이지? 코드가 있으면 더 좋겠다.. 물어보자

### 3. java.time 패키지
* 기존의 날짜처리 클래스(Calendar)는 몇가지 문제점이 존재했다.
	* 불변객체가 아니라 수정될 수 있다.
	* 윤초와 같은 특별한 상황을 고려하지 않는다.
	* 월(month)가 0 ~ 11로 표현한다.
* 따라서 대부분 자바 개발자는 Calendar + Jod-Time이라는 라이브러리를 함께 사용했다.
* java.time패키지에서는 Jodi-Time 라이브러리를 발전시킨 새로운 날짜와 시간에 대한 API를 제공한다.
	
### 4. Optional
* `Optional<T>` 클래스는 T타입의 객체를 포장해주는 Wrapper Class
*  따라서 Optional 인스턴스는 모든 타입의 참조 변수를 저장할 수 있다.
* Optional 객체를 통해 NullPointerException을 간단히 회피할 수 있다.
* `주의` Optional은 데이터를 Wrapping 하거나 null check과정에서 비용이 발생한다.(자원을 사용해서 연산을 한다.)
	* 따라서 Optional을 무분별하게 사용하는 것은 성능저하의 원인이 될 수 있다.
	* 상단 링크 참조

</details>
