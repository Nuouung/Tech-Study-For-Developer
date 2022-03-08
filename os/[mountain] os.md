# Q. 프로세스와 스레드의 차이점
<details>
	<summary>Answer</summary>

프로세스란 실행 중인 프로그램을 의미하며, 운영체제로 부터 자원을 할당받아 동작을 시작하게 됩니다.

반면 스레드는 프로세스로 부터 자원을 할당받아 동작을 시작하게 됩니다. 따라서 모든 스레드는 code, data, heap영역의 메모리 공간을 공유하면서 자신만의 stack, pc register 공간을 가지고 실행됩니다.


</details>

<details>
	<summary>이해하기</summary>

## Reference
*  [스레드 사용이유](https://www.crocus.co.kr/1510) 
*  [스레드 사용이유2](https://beststar-1.tistory.com/6#%EC%8A%A4%EB%A0%88%EB%93%9C_%EC%82%AC%EC%9A%A9_%EC%9D%B4%EC%9C%A0) 
*  [컨텍스트 스위칭](https://beststar-1.tistory.com/26) 
  
## 내용

### 멀티 스레드

* 장점
	* code, data, heap영역을 공유하기 때문에 메모리 공간 절약, 스레드 간 통신비용 절감, 컨텍스트 스위칭으로 인한 오버헤드를 보완할 수 있다.
	* 즉, 멀티 프로세스에 비해 빠르게 처리할 수 있다.

* 단점
	* 공유자원을 사용하기 때문에, 하나의 쓰레드에서 문제가 발생한다면 모든 쓰레드가 영향을 받는다.
	* 또한 공유자원에 대한 동시성 문제도 존재할 수 있다.

### 멀티 프로세스

* 장점
	* 독립적인 처리를 보장할 수 있다. 하나의 프로세스에서 문제가 발생해도 나머지 프로세스에는 영향을 미치지 않는다.

* 단점
	* 멀티 스레드 환경보다 더 많은 메모리 공간을 사용하고, 그로인해 컨텍스트 스위칭으로 인한 오버헤드가 더 크게 발생한다.

</details>

# Q. 컨텍스트 스위칭에대해 설명해주세요.
<details>
	<summary>Answer</summary>

여러개의 프로세스가 동시에 처리될 때, CPU가 해당 프로세스를 실행하기 위한 정보(컨텍스트)를 교체하는 과정을 의미합니다.

컨텍스트 스위칭이 발생시 CPU가 동작하기 때문에 다른 프로세스들은 대기하는 상태가 됩니다. 따라서 잦은 컨텍스트 스위칭은 성능 저하의 원인이 될 수 있습니다.


</details>

<details>
	<summary>이해하기</summary>

## Reference
* [컨텍스트 스위칭](https://beststar-1.tistory.com/26) 
* [프로세스 제어 블록 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4_%EC%A0%9C%EC%96%B4_%EB%B8%94%EB%A1%9D)
* [process control block operating system](https://techmyeducation.blogspot.com/2019/01/process-control-block-operating-system.html)

## 내용

### 컨텍스트란 ?
* CPU가 해당 프로세스를 실행하기 위한 정보.
* 각 프로세스는 PCB(Process Control Block)에 컨텍스트를 저장하게 된다.

###  PCB에 저장되는 정보
![image](https://user-images.githubusercontent.com/26343023/157274635-475d26ea-f1eb-4fb1-86c0-d11e2f76b20e.png)

* Process ID
	* 프로세스를 식별할 수 있는 고유 ID 값
* 프로세스 상태
	* 생성, 준비, 실행, 대기, 완료 상태가 존재 함.
* PC(Program Counter)
	* 해당 프로세스의 다음 명령어 주소를 가리키고 있다.
* CPU 레지스터 및 일반 레지스터
* CPU 스케줄링 정보 
	* 우선 순위, 최종 실행시각, CPU 점유시간 등
* 메모리 관리 정보
	* 해당 프로세스의 주소 공간 등
* 프로세스 계정 정보
	* 페이지 테이블, 스케줄링 큐 포인터, 소유자, 부모 등
* 입출력 상태 정보
	* 프로세스에 할당된 입출력장치 목록, 열린 파일 목록 등


</details>
