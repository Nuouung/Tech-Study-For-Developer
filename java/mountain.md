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
