# JAVA 플랫폼의 3대 구성 요소

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/00899d7f-e178-4759-b195-7d89350d82d3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T034744Z&X-Amz-Expires=86400&X-Amz-Signature=cba54416a9fb9df8c50ac796fa44f76a66b61dbd961ca510348942fe36ad9f28&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 자바 개발 키트 (Java Development Kit, JDK)
- 자바 가상 머신 (Java Virtual Machine, JVM)
- 자바 런타임 환경 (Java Runtime Environment, JRE)

# JDK(**Java Development Kit**)

- 자바 프로그램을 개발하는데 필요한 여러 기능들을 제공한다
    
    ex) java, javac, jar, jre, jvm 
    
- 종류
    1. **Java SE : Java Platform , Standard Edition**
        
        표준 자바 플랫폼으로 표준적인 컴퓨팅 환경을 지원하기 위한 자바 가상머신 규격 및 API 집합을 포함
        
    2. **Java EE : Java Platform , Enterprise Edition**
        
        JavaSE에 웹 어플리케이션 서버에서 동작하는 기능을 추가한 플랫폼
        
        이 스펙에 따라 제품을 구현한 것을 웹 어플리케이션 서버(WAS)라 한다. ex. tomcat
        
    3. **Java ME : Java Platform , Micro Edition**
        
        제한된 자원을 가진 휴대전화, PDA 등에서 Java 프로그래밍 언어를 지원하기 위해 만든 플랫폼 중 하나
        

# JRE (Java Runtime Environment)

- 컴파일된 자바 프로그램을 실행시키기 위해 사용하는 SW로, 자바 클래스 라이브러리(Java class libraries)와 자바 클래스 로더(Java class loader), 자바 가상 머신(Java Virtual Machine)로 구성되어 있다.
- 개발이 아닌 단순 자바 프로그램 실행이 필요하다면 JRE만 설치하면 된다.

# JVM (JAVA Vritual Muchine)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bc1e05db-be51-4d4c-84ca-acfc18065e46/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T034840Z&X-Amz-Expires=86400&X-Amz-Signature=080c9bad895bd9e3ef8d6200e0150047ae5cd1e95955b550f09f0aadc482f4e0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObjectg)

- 일반 프로그램은 OS가 프로그램을 실행시키지만, 자바 프로그램은 OS가 JVM을 실행시키면 JVM이 프로그램(클래스 파일)을 실행시킨다.즉, JVM은 클래스 파일을 실행시켜주는 가상 머신이다
- JAVA는 OS에 의존적이지 않지만, JVM은 H/W와 OS 위에서 실행되기 떄문에 플랫폼에 종속적이다. 따라서 플랫폼에 따라 호환되는 JVM을 실행시켜줘야한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d5e92d09-01ea-4b59-ab83-ce54e82f88a7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T034904Z&X-Amz-Expires=86400&X-Amz-Signature=c1bec2a925a8c8ca3cf5dbdc36187d11f0f5eb5de5e2b18adfcf1f5dd7c74719&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
- 크게 세가지 영역으로 나뉘는데 메모리에 클래스 파일들을 적재하는 Class Loader, OS에게 할당 받은 메모리를 관리하는 Runtime Data Area, 자바 바이트 코드를 읽고 실행하는 Excecution Engine으로 이루어진다.
- 아래에서 하나하나 살펴보도록 하자.
    
    

---

# Class Loader

- 런타임 시점에 클래스 파일들을 JVM 내부로 로딩하고 분석한 뒤 런타임 데이터 영역에 배치한다.
- 특징은 크게 5가지로 나눌 수 있다
    1. 계층 구조
    2. 위임 모델
    3. 가시성 제한
    4. 언로드 불가
    5. 이름 공간 

## 1. 계층 구조/종류

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/13e4530e-dee3-43f3-84fd-8bca4243c6f2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T034927Z&X-Amz-Expires=86400&X-Amz-Signature=405df1c68fe15b149204a3546f310cb2da3a7fa03adac16c63106aa8dcb8a2bc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- Bootstrap Class Loader
    - 최상위 클래스 로더로 JAVA가 아닌 네이티브 코드로 구현되어 있다
    - JVM이 실행될 때 메모리에 같이 올라간다
    - JAVA API들을 로드한다
- Extention Class Loader
    - 기본 JAVA API를 제외한 확장 클래스들을 로드한다
- System Class Loader/Application ClassLoader
    - 어플리케이션의 클래스들을 로드한다
- User-Defined Class Loader
    - 개발자가 직접 코드로 짠 파일들을 JVM에 탑재

## 2. 위임 모델

- 처음 바이트 코드를 넘겨받은 클래스 로더가 필요한 클래스를 로드할 떄 혹은 실행 엔진에서 명령어 단위로 바이트코드를 실행하다가 처음으로 참조하는 클래스에 대해 클래스 로더에게 로드를 요청할 때 로드를 요청받은 클래스 로더는 다음 순서대로 요청 받은 클래스가 있는지 확인한다
    1. 클래스 로더 캐시 
    2. 상위 클래스 로더
    3. 자기 자신 
    
    이전에 로드된 클래스인지 클래스 로더 캐시를 확인하고, 없으면 상위 클래스 로더를 하나씩 거슬러 올라가며 확인하는데 이 때 올라가는 도중에 클래스를 발견하더라도 부트스트랩 클래스 로더까지 확인해서 부트스트랩 클래스 로더에도 해당 클래스가 존재하면 부트스트랩 로더에 있는 클래스를 로드한다. 만약 부트 스트랩 클래스 로더에도 해당 클래스가 없으면 로드를 요청받은 클래스 로더가 파일 시스템에서 해당 클래스를 찾는다. 파일 시스템에도 해당 클래스가 없다면 예외가 발생한다 
    

## 3. 가시성 제한

- 클래스 로더가 클래스 로드를 요청받았을 때 위임 모델에 의해서 클래스 로더 캐시를 확인하고 없으면 상위 클래스 로더를 확인하는데 이 때 하위 클래스 로더에 있는 클래스는 확인이 불가능한 특성

## 4. 언로드 불가

- 클래스를 로드하는 것은 가능하지만 언로드하는 것은 불가능하다

## 5. 이름 공간 (Name Space)

- 각 클래스 로더들이 가지고 있는 공간으로써 로드된 클래스를 보관하는 공간이다. 위임 모델을 통해 상위 클래스 로더들을 확인하는데 그 때 확인하는 공간이 네임스페이스이다.

---

# Runtime Data Areas

- JVM이 OS 위에서 실행되면서 할당받는 메모리 영역으로 클래스 로더에서 분석된 클래스 파일의 데이터를 저장하고 실행 도중에 필요한 데이터를 저장한다. 메모리를 효율적으로 관리하기 위해 크게 PC레지스터, Stack, Method 영역, heap , 네이티브 메소드 스택 등 5개의 영역으로 나눠진다

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8146d1fc-879a-4d81-8b51-34d471f5ac7c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T034944Z&X-Amz-Expires=86400&X-Amz-Signature=2509644fcbf5df2833a9ae0cd68427ef77e5ee7f44761123aff141b869fe3176&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

## PC Register (Program Counter)

- 현재 수행 중인 명령의 주소를 가지며 스레드가 시작될 떄 생성되며 각 스레드마다 하나씩 존재한다

## JVM Stack

- Stack Frame 구조체를 저장하는 스택이다
- 스레드가 시작될 때 생성되며 각 스레드마다 하나씩 존재한다
- 컴파일 시 결정되는 기본형 데이터 타입이 저장되는 공간
- **지역변수, 매개변수, 리턴값, 참조변수** 등이 저장됨
- 메서드 호출될 때, 메모리에 FILO로 하나씩 생성
- 메서드 끝날 때, 메모리에 LIFO로 하나씩 제거
- 메서드 호출시마다 각각의 스택프레임(그 메서드만의 영역)이 생성

## Native Method Stack

- JAVA 외의 언어로 작성된 네이티브 코드를 위한 스택
- JNI(Java Native Interface)를 통해 호출하는 C/C++ 등의 코드를 수행하기 위한 스택으로 언어에 맞게 스택이 생성된다 (C면 C스택, C++이면 C++스텍 생성)

## Heap

- 모든 스레드가 공유한다.
- 런타임시 결정되는 참조형 데이터 타입이 저장되는 공간
- new 연산자를 통해 생성되는 객체가 저장되는영역
- 객체가 더 이상 안쓰이거나, 명시적인 Null 선언시 GC 청소대상이 된다
- JVM 성능 등의 이슈에서 가장 많이 언급되는 공간

## Method(=Class=Static) Area

- 모든 스레드가 공유하는 영역으로 JVM이 시작될 때 생성된다.
- JVM이 읽어 들인 각각의 클래스와 인터페이스에 대한 런타임 상수 풀, 필드와 메서드에 대한 정보, Static 변수, 메서드의 바이트 코드 등을 보관한다
- 구성
    - static zone : static 메서드 저장
    - none-static zone : static 아닌 메서드 저장
- method의 byte code가 저장되는 영역
- 프로그램의 시작부터 종료까지 메모리에 남는다.
- 명시적인 Null 선언시 GC 청소대상

## Runtime Constant Pool

- JVM에서 가장 핵심적인 역할을 수행하는 곳
- 각 클래스와 인터페이스의 상수 뿐만 아니라, 메서드와 필드에 대한 모든 레퍼런스까지 담고 있는 테이블로 어떤 메서드나 필드를 참조할 때 JVM은 런타임 상수 풀을 통해 해당 메서드나 필드의 실제 메모리상 주소를 찾아서 참조한다

# 실행 엔진 (Execution Engine)

---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f56f0474-6605-4d93-b51b-12d3acbafe76/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T035015Z&X-Amz-Expires=86400&X-Amz-Signature=b133319a1ef598fed9ca315577c55b3be562a7230fafccac2f948548b6dda404&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 클래스 로더를 통해 런타임 데이터 영역에 배치된 바이트 코드를 명령어 단위로 읽어서 실행
- 바이트 코드의 각 명령어는 1바이트 크기의 OpCode(Operation Code)와 추가 피연산자로 이루어져 있다. 실행 엔진은 하나의 OpCode를 가져와 피연산자와 작업을 수행 후 다음 OpCode를 수행한다. 이 수행 과정에서 실행 엔진은 바이트 코드를 기계어로 변경한다.
    - 컴파일 방식
        1. 인터프리터 : 바이트 코드 명령어를 한 줄씩 읽어서 해석하고 실행한다. 하나하나의 해석은 빠르지만 전체적인 실행 속도는 느리다. JVM의 기본 동작 방식
        2. JIT 컴파일러(Just-In-Time Compiler) : 자주 반복되는 코드를 네이티브 코드로 변환해 캐싱해놓는다. 네이티브 코드는 캐시에 보관하기 때문에 빠르게 수행된다. 하지만 컴파일 과정이 오래 걸린다 
    
    모든 코드는 초기에 인터프리터 방식을 사용하다가 자주 사용되는 코드를 확인하고 JIT 컴파일러를 사용해 캐싱해둔다. JIT 컴파일러는 JVM의 핵심으로 JVM 내에서 성능에 가장 큰 영향을 준다.
    

# JAVA 코드 실행 과정

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8b4700f3-3012-4be5-869d-d1c506015524/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T035027Z&X-Amz-Expires=86400&X-Amz-Signature=06696c15a06d4aff5cd9b5e9f44ee33e92afea050fac1656cba9c0e6b5e1b779&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 소스 파일(.java)을 자바 컴파일러를 통해 바이트 파일(.class)로 컴파일하고 JVM의 Class Loader에게 전달한다. Class Loader는 필요한 .class 파일들을  불러들이고 코드를 검증한 뒤 JVM내의 Runtime Data Area로 올린다. Runtime Data Area에 있는 .class 파일들은 Execution Engine의 Interpreter와 JIT Complier를 통해 Native Code로 변환된다. 해석된 바이트 코드는 Runtime Data Area 에 배치되어 실질적인 수행이 이루어진다

---

# Garbage Collection

- JVM은 메모리 효율적으로 사용하기 위해  GC를 이용해 힙 영역에서 더이상 사용하지 않는 객체를 제거한다. 어떻게 더이상 사용되지 않는 객체로 인식할까? 객체는 힙 영역에 저장되고 스택 영역에 이를 가리키는 주소값이 저장되는데 참조되지 않는(자신을 가리키는 포인터가 없는, unreachable) 객체를 메모리에서 제거한다.
- JAVA는 Weak Generational Hypothesis 가설로 인해 GC 도입이 가능했다.
    
     Weak Generational Hypothesis는 신규로 생성한 객체의 대부분은 금방 사용하지 않는 상태가 되고, 오래된 객체에서 신규 객체로의 참조는 매우 적게 존재한다는 가설이다. 이 가설에 기반하여 자바는 Young 영역과 Old 영역으로 메모리를 분할하고, 신규로 생성되는 객체는 Young 영역에, 오랫동안 살아남은 객체는 Old 영역에 보관한다.
    

## **Heap 영역**

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8ce800ee-c372-4cdb-b2a9-d7d0bf294f2a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T035039Z&X-Amz-Expires=86400&X-Amz-Signature=71caa0c3ada1a6eb0e819ec770d2a649b05509559e8f78130a9ba8e41f1bbe96&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

1. Young generation
    - 새롭게 생성한 객체가 위치한다. 대부분의 객체가 금방 접근 불가능 상태(Unreachable)가 되기 때문에 많은 객체가 Young 영역에 생성되었다가 사라진다. 이 영역에서 객체가 사라질 때 Minor GC 가 발생한다고 말한다.
    - 각 객체는 Minor GC에서 살아남은 횟수를 기록하는 age bit 를 가지고 있다. Minor GC가 발생할 때마다 age bit 값은 1씩 증가 하게되며, age bit 값이 MaxTenuringThreshold 라는 설정값을 초과하게 되는 경우 Old Generation 영역으로 객체가 이동한다. Age bit가 MaxTenuringThreshold 초과하기 전이라도 Survivor 영역의 메모리가 부족할 경우에는 미리 Old Generation 으로 객체가 옮겨질 수도 있다.
        - Eden
            - 새로 생성된 객체들이 위치한다.
            - 영역이 꽉차면 Minor GC 발생하는데 이 때 참조되지 않는 객체는 메모리에서 제거되고 사용중인 객체는 Survivor 영역으로 옮겨진다
        - Survivor 1,2
            - Eden 영역에서 GC 실행 후 살아남은 객체들이 위치한다.
            - 영역이 꽉차면 Minor GC 발생하는데 이 때 참조되지 않는 객체는 메모리에서 제거되고 사용중인 객체는 다른  Survivor 영역으로 옮겨진다(Promotion)
            - Minor GC가 발생할 때마다 Survivor1 영역에서 Survivor2 영역으로 또는 Survivor2 영역에서 Survivor1 영역으로 객체가 이동한다
            - 객체의 생존 횟수를 카운트하기 위해 Minor GC에서 객체가 살아남은 횟수를 의미하는 age를 Object Header에 기록한다. 그리고 Minor GC 때 Object Header에 기록된 age를 보고 Promotion 여부를 결정한다.
2. Old generation
    - Suvivor 영역에서 여러번의 GC 후 살아남은 객체들이 위치한다. 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다. 이 영역에서 객체가 사라질 때 Major GC(Full GC) 가 발생한다.
    - 예외적인 상황으로 Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우도 존재한다. 이러한 경우를 대비하여 Old 영역에는 512 bytes의 덩어리(Chunk)로 되어 있는 카드 테이블(Card Table)이 존재한다.
        
        카드 테이블에는 Old 영역에 있는 객체가 Young 영역의 객체를 참조할 때 마다 그에 대한 정보가 표시된다. Young 영역에서 가비지 컬렉션(Minor GC)가 실행될 때 모든 Old 영역에 존재하는 객체를 검사하여 참조되지 않는 Young 영역의 객체를 식별하는 것이 비효율적이기 때문에 Young 영역에서 가비지 컬렉션이 진행될 때 카드 테이블만 조회하여 GC의 대상인지 식별할 수 있도록 한다.
        
3. Permanet 영역
    - JDK8부터 Permanet 은 Metaspace로 교체됐다.
    - Metaspace 영역은 Heap이 아닌 Native 메모리 영역으로 취급하게 된다. Heap 영역은 JVM에 의해 관리된 영역이며, Native 메모리는 OS 레벨에서 관리하는 영역으로 구분된다. 그 결과 기존과 비교해 큰 메모리 영역을 사용할 수 있게 되었다.
    

## **GC 방식**

- JVM 버전이 올라감에 따라 여러가지 GC방식이 추가되고, 발전되어 왔다
- 기본 개념
    - Mark-sweep-compact 알고리즘
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/25e492a0-5f67-4014-bde8-53950316f0c0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T035103Z&X-Amz-Expires=86400&X-Amz-Signature=63a7b5822351a5169a6bc2dd7a3a448199a8ba9a39ff91f8ebb341f2a2d31f59&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
        
        - 다양한 GC에서 사용되는 기본적인 GC 과정이다.  GC 대상객체를 식별하고 제거하며 객체가 제거되어 파편화된 메모리 영역을 앞에서부터 채워나가는 작업을 수행하게 된다.
            
            사용되지 않는 객체를 식별하고 (**Mark**) 
            
            사용되지 않는 객체를 제거하고 (**Sweep**) 
            
            파편화된 메모리 영역을 앞에서부터 채워나간다 (**Compaction**)
            
    - Stop-The-World
        - GC를 처리하는 동안 GC를 실행하는 스레드를 제외한 모든 스레드가 중단되는 현상
        - GC의 성능 개선을 위해 튜닝을 한다고 하면 보통 stop-the-world의 시간을 줄이는 작업을 한다
- 종류
    1. Serial GC
        - Mark-sweep-compact 알고리즘이 수행된다.
        - CPU 코어 갯수가 1개일 때 사용한다
    2. Paraller GC
        - Serial GC와 알고리즘은 같지만 GC를 여러개의 Thread로 처리해 Stop-The-World 현상이 나타나는 시간이 줄였다
        - 메모리와 CPU 코어가 충분할 때 적합하다.
        - Java8까지 기본 가비지 컬렉터(Default Garbage Collector)로 사용되었다
    3. Paraller Old GC
        - Paraller GC에서 Old GC 알고리즘을 개선한 버전이다.
        - Mark-Summary-Compaction 알고리즘을 사용하는데 이 알고리즘은 Old GC 처리량을 늘려주기위해 Summary 단계에서는 이미 GC가 수행된 영역에 살아있는 객체를 식별하는 작업을 진행한다
    4. CMS GC 
        
        - Java9 버젼부터 deprecated 되었고 Java14에서는 사용이 중지되었다
        - 앞선 방식들보다 좀 더 개선된 방식으로 Mark Sweep 알고리즘을 Concurrent하게 수행해 STW시간을 최소화하기 위해 고안됐다
        - GC 대상을 최대한 자세히 파악한 후, 정리하는 시간(STW가 발생하는 시간)을 짧게 가져간다. GC 대상을 파악하는 과정이 복잡하한 여러 단계로 수행되기 때문에 다른 GC 대비 CPU 사용량이 높다
        - 동작 과정
            - **Initial Mark**
                - GC 과정에서 살아남은 객체를 탐색하는 시작 객체(GC Root)에서 참조 Tree상 가까운 객체만 1차적으로 찾아가며 객체가 GC 대상(참조가 끊긴 객체)인지를 판단한다. 이 때는 STW 현상이 발생하게되지만, 탐색 깊이가 얕기 때문에 STW 발생 기간이 매우 짧다.
            - **Concurrent Mark**
                - STW 현상 없이 진행되며, Initial Mark 단계에서 GC 대상으로 판별된 객체들이 참조하는 다른 객체들을 따라가며 GC 대상인지를 추가적으로 확인한다.
            - **Remark**
                - Concurrent Mark 단계의 결과를 검증한다. Concurrent Mark 단계에서 GC 대상으로 추가 확인되거나 참조가 제거되었는지 등등을 확인 한다. 이 과정은 STW 를 유발하기 때문에 STW 지속시간을 최대한 줄이기 위해 멀티스레드로 검증 작업을 수행한다.
            - **Concurrent Sweep**
                - STW 없이 Remark 단계에서 검증 완료된 GC 객체들을 메모리에서 제거한다.
        1. G1 GC (G1: Garbage First)
            
            ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ea99602a-5e44-40ba-8326-1a7a4e8f994c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T035125Z&X-Amz-Expires=86400&X-Amz-Signature=aea7757ee4bf8758d85940097b5980f39699c27e1f2c20d868b11690a967d5f6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
            
            - Java9부터 기본 가비지 컬렉터(Default Garbage Collector)로 사용
            - 큰 힙 메모리에서 짧은 GC 시간을 보장
            - 전체 힙 메모리 영역을 Region 이라는 균등한 크기로 나눠서 각 Region을 역할과 함께 논리적(Eden, Survivor, Old)으로 구분하고 가비지가 많은 Region을 우선적으로 GC를 수행한다
                - Humonguous : Region 크기의 50%를 초과하는 객체를 저장하는 Region
                - Availabe/Unused : 사용되지 않은 Region
            - 동작
                - Minor GC
                    
                    한 지역에 객체를 할당하다가 해당 지역이 꽉 차면 다른 지역에 객체를 할당하고, Minor GC가 실행된다. G1 GC는 각 지역을 추적하고 있기 때문에, 가비지가 가장 많은(Garbage First) 지역을 찾아서 Mark and Sweep를 수행한다. Eden 지역에서 GC가 수행되면 살아남은 객체를 식별(Mark)하고, 메모리를 회수(Sweep)한다. 그리고 살아남은 객체를 다른 지역으로 이동시키게 된다. 복제되는 지역이 Available/Unused 지역이면 해당 지역은 이제 Survivor 영역이 되고, Eden 영역은 Available/Unused 지역이 된다.
                    
                - Major GC(Full GC)
                    
                    시스템이 계속 운영되다가 객체가 너무 많아 빠르게 메모리를 회수 할 수 없을 때 Major GC(Full GC)가 실행된다. 기존의 다른 GC 알고리즘은 모든 Heap의 영역에서 GC가 수행되었으며, 그에 따라 처리 시간이 상당히 오래 걸렸다. 하지만 G1 GC는 어느 영역에 가비지가 많은지를 알고 있기 때문에 GC를 수행할 지역을 조합하여 해당 지역에 대해서만 GC를 수행한다. 그리고 이러한 작업은 Concurrent하게 수행되기 때문에 애플리케이션의 지연도 최소화할 수 있다.
                    
            - Young GC를 수행할 때는 STW현상이 발생하기 떄문에 시간을 최대한 줄이기 위해 멀티스레드로 GC를 수행한다. Young GC는 각 Region 중 GC대상 객체가 가장 많은 Region(Eden 또는 Survivor) 에서 수행되며, 이 Region 에서 살아남은 객체를 다른 Region(Survivor) 으로 옮긴 후, 비워진 Region을 사용가능한 Region으로 돌리는 형태로 동작한다.
                - 동작 과정
                    
                    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1a6751ef-4ef9-4a66-9e63-f25a0e1187e0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220219%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220219T035153Z&X-Amz-Expires=86400&X-Amz-Signature=0dc95a0dacea97235189f0e0a5bfc0b8125aef8b44e06576fe1f79406c0110d0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
                    
                    1. Initial Mark
                        - Old Region 에 존재하는 객체들이 참조하는 Survivor Region 을 찾는다. 이 과정에서 STW 현상이 발생한다.
                    2. Root Region Scan
                        - Initial Mark 에서 찾은 Survivor Region에 대한 GC 대상 객체 스캔 작업을 진행한다.
                    3. Concurrent Mark
                        - 전체 힙의 Region에 대해 스캔 작업을 진행하며, GC 대상 객체가 발견되지 않은 Region 은 이후 단계를 처리하는데 제외한다.
                    4. Remark
                        - STW 상태에서 최종적으로 GC 대상에서 제외될 객체(살아남을 객체)를 식별한다.
                    5. Cleanup
                        - STW 상태에서 살아있는 객체가 가장 적은 Region 에 대한 미사용 객체 제거 수행한다. 이후 STW를 끝내고, 앞선 GC 과정에서 완전히 비워진 Region 을 Freelist에 추가하여 재사용될 수 있게 한다.
                    6. Copy
                        - GC 대상 Region이었지만 Cleanup 과정에서 완전히 비워지지 않은 Region의 살아남은 객체들을 새로운(Available/Unused) Region 에 복사하여 Compaction 작업을 수행한다.
