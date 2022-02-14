## 일러두기1

블로그 게시글로 보시면 더욱 쾌적한 UI를 경험하실 수 있습니다. 


[블로그 게시글로 가기](https://gaebalsogi.tistory.com/64)


## 일러두기2


본 글은 유튜브 우아한Tech의 [\[10분 테코톡\] 👌던의 JVM의 Garbage
Collector](https://www.youtube.com/watch?v=vZRmCbl871I&t=744s)와 망나니개발자님의
티스토리 게시글
<span style="background-color: #ffffff; color: #000000;">[\[Java\]
Garbage Collection(가비지 컬렉션)의 개념 및 동작 원리
(1/2)](https://mangkyu.tistory.com/118),
[YABOONG님의](https://yaboong.github.io/java/2018/06/09/java-garbage-collection/)
</span>[자바 메모리 관리 - 가비지
컬렉션](https://yaboong.github.io/java/2018/06/09/java-garbage-collection/)을
<span style="background-color: #ffffff; color: #000000;">보고 해당 내용을 정리한
글입니다.</span>

 

 

 

 

## <span style="color: #000000;"><span style="background-color: #ffffff;">JVM</span></span>

> 자바 가상 머신(영어: Java Virtual Machine, JVM)은 [자바
> 바이트코드](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EB%B0%94%EC%9D%B4%ED%8A%B8%EC%BD%94%EB%93%9C)를
> 실행할 수 있는 주체이다.
> 일반적으로 [인터프리터](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%ED%94%84%EB%A6%AC%ED%84%B0)나 [JIT
> 컴파일](https://ko.wikipedia.org/wiki/JIT_%EC%BB%B4%ED%8C%8C%EC%9D%BC) 방식으로
> 다른 컴퓨터 위에서 바이트코드를 실행할 수 있도록 구현되나 jop [자바
> 프로세서](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%ED%94%84%EB%A1%9C%EC%84%B8%EC%84%9C)처럼
> 하드웨어와 소프트웨어를 혼합해 구현하는 경우도 있다. (이론적으로는 100% 하드웨어 구현도 가능하나 비효율적이다) 자바
> 바이트코드는 플랫폼에 독립적이며 모든 자바 가상 머신은 자바 가상 머신 규격에 정의된 대로 자바 바이트코드를
> 실행한다. 따라서 표준 자바 API까지 동일한 동작을 하도록 구현한 상태에서는 이론적으로 모든 자바 프로그램은
> CPU나 운영 체제의 종류와 무관하게 동일하게 동작할 것을 보장한다.  
>   
> \- 위키백과, 자바 가상 머신  
> [출처](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EA%B0%80%EC%83%81_%EB%A8%B8%EC%8B%A0)

 

<span style="background-color: #ffffff; color: #202122;">JVM은 자바 코드를
해석하는 주체로, 운영체제의 메모리 영역에 접근해 메모리를 관리하는 프로그램이다. Java라는 프로그래밍 언어가
갖는 가장 큰 특징 중 하나가 운영체제에 종속되지 않고 플랫폼으로부터 독립적이라는 것인데 이를 가능하게 하는 것이 바로
JVM이다. JVM은 자신이 설치되어 있는 운영체제가 윈도우이던, 리눅스이던 혹은 maxOS이던 상관 없이 동일한 Java
문법으로 작성된 코드가 각각의 모든 플랫폼에서 동작될 수 있도록 보장한다. (이와 같은 일이 가능한 이유는 JVM
위에 각각의 OS에 맞는 JRE, 즉 Java Runtime Environment가 올라가기 때문이다.)</span>

 

Java의 모든 동작은 JVM을 통해 수행된다. 즉, OS의 메모리 영역에 접근할 때 Java가 직접 접근하는 것이 아니라
JVM이라는 가상머신을 거쳐 접근하는 것. JVM은 C로 쓰여진 하나의 프로그램이기 때문에 특정한 동작을 수행할 수 있고
메모리를 사용자가 직접 관리하는 것은 매우 까다로운 주제이기 때문에 JVM은 사용자를 대신해 동적인 메모리를 관리하는
작업을 수행한다. Garbage Collector는 JVM이 동적인 메모리를 추적, 삭제하는 기전이다.

<span style="color: #202122;"><span style="background-color: #ffffff;"> </span></span>

 

 

 

## <span style="color: #202122;"><span style="background-color: #ffffff;">Garbage Collector</span></span>

<span style="color: #202122;"><span style="color: #202122;"><span style="background-color: #ffffff;">Garbage
Collector를 이해하기 위해서는 메모리 영역, 구체적으로는 힙과 스택 영역에 대해 알 필요가 있다. 왜냐하면 Garbage
Collector는 'Heap 영역의 오브젝트 중 stack에서 도달 불가능한 객체들을 추적하고 제거하는 기전'이기 때문이다.
만약 힙과 스택에 대해 정확한 이해가 되지 않는다면, </span></span></span>[메모리구조 기초 :
힙(heap)영역과 스택(stack)영역을
중심으로](https://gaebalsogi.tistory.com/16?category=995740)를 한번
확인해보자. 요약해 이야기하자면 Garbage Collector는 힙영역에 존재하지만 더이상 스택영역에서 참조하지
않는 객체를 주 제거 대상으로 삼는다.

 

  - Heap : **동적으로 할당된 메모리 영역.** 자바의 경우 모든 Object 타입의 데이터가 할당되며, Heap 영역의
    Object를 가리키는 참조 변수는 stack 영역에 할당된다.
  - stack : **정적으로 할당된 메모리 영역.** 원시 타입의 데이터가 할당되는 영역이며, Heap 영역에 생성된
    Object 타입의 데이터의 참조 값이 할당된다.

 

아래의 예시를 한번 보자.

``` java
// deliciousCake이라는 이름을 갖는 Cake 객체를 선언한다.
// 이때, deliciousCake의 참조값(객체의 위치를 나타내는 값이라고 보면 된다)은 stack에
// 생성된 Cake 객체는 heap에 할당된다.
Cake deliciousCake = new Cake();

// 아래의 코드로 deliciousCake이 더이상 heap 내의 Cake 객체를 가리키지 않게 되었다.
deliciousCake = null;

// Garbage 생성 (heap 내의 Cake 객체가 더이상 도달 가능하지 않기 때문에)
```

 

 

 

 

## Garbage Collector의 동작 원리 : Minor GC와 Major GC

JVM의 힙영역은 Young Generation과 Old Generation으로 나눌 수 있다. 그리고 Young
Generation은 다시 Eden, Survivor 0, Survival 1으로 나눌 수 있다. 아래의 그림을 한번 보자.

 

![img](http://www.waitingforcode.com/off-heap/on-heap-off-heap-storage/read)

 

동적으로 할당되는 메모리는 최초에 Eden 영역에 할당되며 생존의 시간이 길면 길수록 Old Generation측으로 옮겨진다.
즉, 오랫동안 참조되는 객체는 살아남아 Survival 0, 1을 지나 Old Generation으로, 더 이상 참조되지 않는
객체는 Garbage Collector에 의해 제거되는 그런 동작 원리를 지니는 것이다.

 

아래는 Young Generation과 Old Generation, 그리고 Garbage Collector의 구체적인 동작과정을
나타낸다.

 

#### Young Generation

  - 새롭게 생성된 객체가 할당되는 영역이다.
  - 대부분의 객체는 도달할 수 없는 상태, 즉 참조되지 않는 상태가 되기 때문에 많은 객체가 이곳에서 사라진다.
  - Eden 영역이 한번 가득차면 Garbage Collector가 실행되는데 이 때 실행되는 가비지 컬렉션을 Minor
    GC라고 부른다.
  - Eden 영역에서 살아남은 객체는 Survival 0 혹은 1로 가게된다. 이 때 Survival 0, 1 중 하나는
    반드시 비어 있다.

 

#### Old Generation

  - Young Generation에서 살아남은(참조값이 유지되는) 객체가 위치하는 영역이다.
  - Old Generation이 가득차면 Garbage Collector가 실행되는데 이 때 실행되는 가비지 컬렉션을
    Major GC 혹은 Full GC라고 부른다.

 

#### Garbage Collector 동작 과정

1.  새로운 객체가 Eden 영역에 할당된다. 이 때 두개의 Survival 중 하나는 반드시 비워진 상태로 시작된다.
2.  Eden 영역이 가득차면 Minor GC가 발생한다.
3.  Minor GC에서 참조값이 유지된 객체는 Survival 영역으로 이동한다. 참조값이 존재하지 않는 객체는 Minor
    GC 중 메모리에서 삭제된다.
4.  다음 Minor GC가 발생할 때, Eden 영역에서는 3번과 같은 과정이 반복된다. 기존에 Survival 영역에
    위치하던 객체들 중 참조값이 유지된 객체들은 다른 Survival 영역으로 이동하며 이때 객체의 age값이
    1 증가한다. Survival 영역에서 참조값이 존재하지 않게 된 객체는 메모리에서 삭제된다.
5.  4번의 과정이 반복되며, 이 과정에서 지속적으로 살아 남은 객체 중 age 값이 특정 값 이상인 객체들은 Old
    Generation으로 옮겨진다. Young Generation에서 Old Generation으로 객체가 이동하는 단계를
    Promotion이라고 이야기한다.
6.  Minor GC의 반복과 Promotion 작업의 반복이 계속 일어나다 보면 Old Generation이 가득차게 된다.
7.  이 때 Major GC가 발생한다.

Garbage Collector 동작 과정은 [자바 메모리 관리 - 가비지
컬렉션](https://yaboong.github.io/java/2018/06/09/java-garbage-collection/)
게시글을 참고했다.

 

 

 

## Garbage Collector의 두가지 동작 방식

####  

####  

#### Stop The World

Stop The World는 가비지 컬렉션이 실행될 때, 가비지 컬렉션을 실행하는 특정 스레드를 제외한 모든 스레드의 작업을
중단하는 동작 방식이다. 이 과정이 실시되면 가비지 컬렉션이 수행되는 동안 애플리케이션의 모든 동작이 중단된다.

 

 

 

#### Mark and Sweep

Mark and Sweep은 말 그대로 mark, 사용되는 메모리와 사용되지 않는 메모리를 식별한 후에 sweep, 사용되지 않는
메모리를 제거하는 동작 방식이다.
