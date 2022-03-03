## 1. 컴파일 언어
![](https://images.velog.io/images/tlsrlgkrry/post/f0137629-17f5-4086-805a-345a058d3bb2/image.png)
### 1-1. 실행과정🔎 
1. 소스코드 작성
2. 컴파일러를 통해 기계어(2진 코드)로 변환
3. CPU에서 실행

### 1-2. 특징📌
- 기계어로 컴파일된 실행파일을 실행하기 때문에 실행속도가 빠르다.
- 코드를 수정하면 다시 컴파일 과정을 거쳐야 한다.
- 운영체제 이식성이 낮다.
	➡️ OS마다 실행 할 수 있는 기계어가 다른 경우가 있다. 그러므로 해당 OS에 맞는 컴파일러로 다시 컴파일 해야한다.
- 번역과 실행이 완전히 따로 이루어진다.
- C, C++등이 있다.



---
## 2. 인터프리터 언어
![](https://images.velog.io/images/tlsrlgkrry/post/dd1c5296-7947-4100-9fd9-b507d94d9632/image.png)

### 1-1. 실행과정🔎 
1. 소스코드 작성
2. 컴파일러를 통해 기계어(2진 코드)로 변환
3. CPU에서 실행

### 1-2. 특징📌
- 컴파일 과정이 없어서 실행속도가 느리다.
- 실행 파일이 만들어지지 않는다.
- 운영체제 이식성이 높다.
	➡️ OS마다 호환되는 인터프리터만 준비되어 있다면 바로 실행이 가능하다!
- 한번에 한줄씩 읽어 번역(JVM), 실행(CPU)가 동시에 일어난다.
- Java, JavaScript가 있다.


---

## 3. 표로 한번에 정리
|구분|컴파일러|인터프리터|
|:---:|:---:|:---:|
|번역 단위|전체|줄|
|실행 파일|생성|생성 X|
|실행 속도|빠름|느림|
|번역 속도|느림|빠름|

# 1. 자바의 실행과정
자바는 컴파일 언어이기도 하고 인터프리터 언어이기도 하다. 
컴파일 언어와 인터프리터 언어가 어떻게 혼용 될 수 있었을까?? 자바의 실행과정을 보자!!
![](https://images.velog.io/images/tlsrlgkrry/post/17097144-4d88-49bc-9b09-cc3184d5cc20/image.png)(출처: https://st-lab.tistory.com/176)

1. Java 컴파일러(javac)가 Java 소스코드(.java)를 읽어들여 Java 바이트코드(.class)로 변환시킨다.<span style="color:orange">(컴파일 언어)</span>
2. Class Loader를 통해 .class파일들을 JVM으로 로딩한다.
3. 로딩된 class파일들은 Execution Engine을 통해 해석된다.
이때 실행엔진(Execution Engine)은 두가지 방식 (인터프리터, JIT 컴파일러)으로 진행된다. <span style="color:orange">(인터프리터 언어)</span>
4. 해석된 바이트코드는 Runtime Data Areas에 배치되어 실질적인 명령어 수행이 이루어지게 된다.
5. 위와 같은 과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.

---
# 2. JVM
## 2-1. JVM이란?
JVM이란 Java Virtual Machine, 자바 가상 머신의 약자를 따서 줄여 부르는 용어로 <span style='color: orange'>JAVA와 OS사이에서 중개자 역할을 수행</span>하여 OS에 구애받지 않고 재사용할 수 있게 도와준다.

## 2-2. JVM의 구성
### 1. Class Loader (클래스 로더)
자바는 동적 로드, 즉 컴파일 타임이 아니라 런타임(바이트 코드를 실행할 때)에 클래스 로드하고 링크하는 특징이 있다. Class Loader가 <span style='color: orange'>RunTime 시점에 클래스를 로딩</span>하게 해주며 클래스의 인스턴스를 생성하거나 static키워드를 사용했을 때 클래스가 로딩된다.

### 📌 Class Loader의 특징 📌

**<span style='color: #13AC6B'>1. 계층구조 (Hierarchical)</span>**
Class Loader끼리 부모, 자식관계를 이루어 계층 구조를 형성하며 최상위 클래스 로더는 Bootstrap Class Loader이다. ![](https://images.velog.io/images/tlsrlgkrry/post/3c09125a-e6e8-4513-9523-638e15a1bf2a/image.png)(출처: https://www.ibm.com/developerworks/java/library/j-dclp1/index.html?S_TACT=105AGX02&S_CMP=EDU)
- <span style='color: orange'>Bootstrap Class Loader </span>
: 자바 가상 머신이 실행될때 **가장 먼저 실행되는 클래스 로더**로 자바 런타임 코어 클래스를 로드한다. 필요한 클래스를 로드할 수 있게 최소한의 필수 클래스(java.lang.Object, Class, ClassLoader) 만 로드한다.

- <span style='color: orange'>Extension Class Loader </span>
: 기본 자바API를 제외한 확장 클래스가 로드된다.

- <span style='color: orange'>System Class Loader</span>
: 애플리케이션의 클래스를 로드한다. 사용자가 지정한 $CLASSPATH내의 클래스를 로드한다. 
`-cp`, `-classpath` 를 통해 지정이 가능하다.

- <span style='color: orange'>User-Defined Class Loader</span>
: 애플리케이션 레벨에서 사용자가 직접 코드 상으로 생성한 클래스 로더이다.

**<span style='color: #13AC6B'>2. 위임모델 (Delegation Model)</span>**
어떠한 클래스 파일을 로딩할 때, 해당 로딩 요청이 부모 클래스 로더들로 거슬러 올라가 BootstrapClassLoader(최상위 ClassLoader)에 다다른 후 그 밑으로 로딩 요청을 수행 ![](https://images.velog.io/images/tlsrlgkrry/post/41cb7ea3-2dca-40a9-9cb7-1cb518683c3d/image.png)(출처 : https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)

**<span style='color: #13AC6B'>3. 언로드 불가 (Unload Impossibility)</span>**
클래스 로더에 의해 로딩된 클래스들은 JVM 상에서 삭제할 수 없다
Unloading 기능을 우회적으로 구현하는 방법은 Class를 로드한 Class Loader 자체를 삭제하고,
새로운 Class Loader를 만들어서 다시 Class를 로드하면, reload 되는 것처럼 작동하는 것이 된다.


### 2. Runtime Data Areas (메모리)
![](https://images.velog.io/images/tlsrlgkrry/post/2432c66f-f6f3-4164-aafc-d101f083164d/image.png)(출처: https://d2.naver.com/helloworld/1230)

프로그램을 수행하기 위해 OS에서 할당받은 메모리 영역이며 Class Loader에서 준비한 데이터들을 보관하는 저장소이다. 
PC Register, JVM Stack, Native Method Stack은 각 스레드마다 생성되고 Heap, Method Area, Runtime Constant Pool은 모든 스레드가 공유한다.


- <span style='color: orange'>PC Register</span>
: 현재 쓰레드가 실행되는 명령어의 주소를 저장 (CPU의 PC Register와는 상관없다)
- <span style='color: orange'>JVM Stack</span>
: 프로그램 실행과정에서 임시로 할당되었다가 메소드를 빠져나가면 소멸되는 데이터를 저장하기 위한 영역이다. 지역변수, 매개변수, 리턴값 및 연산 시 일어나는 값들을 임시로 저장한다.
- <span style='color: orange'>Native Method Stack</span>
: 자바 이외의 언어로 작성된 Native Code를 위한 영역이다. 일반적인 메소드를 실행하는 경우 JVM 스택에 쌓이다가 해당 메소드 내부에 네이티브 방식을 사용하는 메소드(예를 들면 C언어로 작성된 메소드)가 있다면 해당 메소드는 네이티브 스택에 쌓인다.
- <span style='color: orange'>Heap</span>
: 객체를 저장하는 가상 메모리 공간이다. new 연산자로 생성된 객체와 배열을 저장한다. Garbage Collector는 힙 영역을 청소하여 메모리를 확보하고 참조하는 변수나 필드가 없다면 의미 없는 객체가 되어 GC의 대상이 된다
- <span style='color: orange'>Method Area( =Class Area =Static Area )
</span> : 클래스 정보를 처음 메모리 공간에 올릴 때 초기화 되는 대상을 저장하기 위한 메모리 공간이다. Method Area는 클래스 데이터를 위한 공간이라면 Heap영역은 객체를 위한 공간이다. Heap과 마찬가지로 GC의 관리 대상에 들어간다. 
저장되는 정보는 다음과 같다.
1 ) **Field information** : 변수의 이름, 타입, 접근 제어자 정보
2 ) **Method information** : 함수의 이름, 타입, 접근 제어자 정보
3 ) **Type information** : class 인지 interface인지, ...

- <span style='color: orange'>Runtime Constant Pool
</span> : 각 클래스와 인터페이스의 상수뿐만 아니라, 메서드와 필드에 대한 모든 레퍼런스까지 담고 있는 테이블이다. 즉, 어떤 메서드나 필드를 참조할 때 JVM은 런타임 상수 풀을 통해 해당 메서드나 필드의 실제 메모리상 주소를 찾아서 참조한다. Method Area에 포함되는 영역이다.



### 3. Execution Engine (실행 엔진)
Execution Engine은 Class Loader를 통해 JVM 내의 Runtime Data Areas에 배치된 바이트코드를 명령어 단위로 읽어서 실행한다.

- <span style='color: orange'>Interpreter
</span>: 바이트코드 명령어를 하나씩 읽어서 해석하고 실행한다. 각각의 해석은 빠르지만 인터프리터 결과의 실행은 느리다는 단점을 갖고있다.

- <span style='color: orange'>JIT(Just-In-Time) Compiler
</span>: 인터프리터의 단점을 보완하기 위해 도입된 것이 JIT 컴파일러이다. 인터프리터 방식으로 실행하다가 **컴파일 임계치**(JVM 내에 있는 메소드가 호출된 횟수 + 메소드가 루프를 빠져나오기까지 회전한 횟수)를 초과하면 해당 바이트코드 영역를 컴파일하여 네이티브 코드로 변경하여 캐시에 보관한다. 

물론 JIT컴파일러가 컴파일하는 과정은 바이트코드를 인터프리팅하는 것보다 훨씬 오래걸리므로 한 번만 실행되는 코드라면 컴파일하지 않고 인터프리팅하는 것이 유리하다.