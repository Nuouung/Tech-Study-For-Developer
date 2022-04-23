# Q. Web과 Was의 차이점 ?
<details>
	<summary>Answer</summary>

Web서버는 정적인 컨텐츠를 처리하고 WAS는 동적인 컨텐츠를 제공하기 위한 서버입니다.

Web과 Was를 기능에 따라 분리함으로써 자원 이용의 효율성을 높일 수 있고, 장애 극복, 배포 및 유지보수의 편의성을 높일 수 있다는 장점을 가지게 됩니다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [Web Web Server와 WAS의 차이와 웹 서비스 구조 - Heee’s Development Blog](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)

</details>

# Q. 공개키, 비밀키 암호화
<details>
	<summary>Answer</summary>

* 공개키 암호화 방식 비밀키로만 열어볼 수 있습니다. 따라서 데이터를 암호화해야하는 경우 사용됩니다.
* 반면 비밀키 암호화 방식은 공개키를 가진 누구나 확인할 수 있습니다. 하지만 클라이언트 입장에서는 인증된 공개키로 데이터를 열람할 수 있다는 것은 송신자를 신뢰할 수 있다는 의미이기 때문에 전자 서명과 같은 경우에 사용됩니다.


</details>

<details>
	<summary>이해하기</summary>

## Reference
* [HTTPS와 SSL 인증서 - 생활코딩](https://opentutorials.org/course/228/4894)
  

</details>

# Q. Immutable
<details>
	<summary>Answer</summary>
Immutable은 불변 객체를 의미합니다. 생성 후 변경할 수 없다는 의미이고 final class로 불변 클래스를 정의할 수 있습니다.
Java에서는 대표적으로 String이나 Wrapper클래스들이 모두 불변 객체로 사용되고 있습니다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [Immutable class in java and immutable objects - JavaGoal](https://javagoal.com/immutable-class-in-java/)
  

</details>


# Q. 캐시 메모리 ?
<details>
	<summary>Answer</summary>

캐시 메모리는 속도가  빠른 장치와 느린 장치의 속도 차이에 따른 병목 현상을 줄이기 위한 범용 메모리 입니다.
메인 메모리에서 자주 사용되는 데이터를 저장하기 위해 지역성을 이용해 예측할 수 있습니다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [운영체제(OS) 10. 캐시 메모리(Cache Memory)](https://rebro.kr/180)
* [tech-interview-for-developer/캐시 메모리(Cache Memory).md at master · gyoogle/tech-interview-for-developer · GitHub](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Computer%20Architecture/%EC%BA%90%EC%8B%9C%20%EB%A9%94%EB%AA%A8%EB%A6%AC(Cache%20Memory).md)  

## 내용

지역성이란 데이터에 대한 접근이 시간적, 공간적으로 가깝게 발생하는 것을 의미하며 캐시의 적중률을 극대화하여 효율성을 높여준다.

공간적 지역성은 배열, 시간적 지역성은 for나 while같은 반복문을 예시로 들 수 있다.

* 공간 지역성: 최근에 사용한데이터 근처에서 참조될 가능성이 높다.
* 시간 지역성: 최근에 사용한 데이터가 재참조 될 가능성이 높다.

</details>
