# Q. JPA와 MyBatis의 공통점과 차이점

<details>
	<summary>Answer</summary>

## 공통점
* Java 진영의 Persistence Framework 이다.
	* Persistence Framework란 데이터의 저장, 조회, 변경, 삭제를 다루는 클래스 및 설정 파일들의 집합.

## 차이점
* MyBatis는 SQL Mapper.
	* `SQL을 사용`해 직접 데이터베이스를 다룬다. 

* JPA는 ORM (Object-Relational Mapper)
	* 객체와 테이블을 매핑한다.
		* 객체는 객체대로, 관계형 데이터베이스는 관계형 데이터베이스대로 설계하면 ORM프레임워크가 중간에서 매핑해준다.
	* `SQL 중심적인 개발에서 객체 중심으로 개발할 수 있다.`

SQL Mapper는 Java코드와 SQL코드를 분리할 수 있고, 복잡한 Join쿼리나 튜닝을 유연하게 사용 할 수 있다. 

하지만 단순한 CRUD SQL작성이 반복되고, 데이터베이스 설정이 변경되면 소스코드의 변경도 많아진다. 또한 특정 DB에 종속적이다.

반면 ORM 프레임워크는 반복적인 CRUD의 작업을 줄여주어 개발의 생산성을 높일 수 있고, 유지보수가 편리해진다. 또한 `성능 최적화 기능`을 제공한다.

또한 동일한 코드를 간단한 설정(Dialect)변경으로 다양한 DB에서 사용가능하다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [자바 ORM 표준 JPA 프로그래밍 - 기본편 - 인프런 | 강의](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)
* [지속성 프레임워크 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EC%A7%80%EC%86%8D%EC%84%B1_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)
* [객체 관계 매핑 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EA%B0%9D%EC%B2%B4_%EA%B4%80%EA%B3%84_%EB%A7%A4%ED%95%91)  

## 내용

### JPA의 성능 최적화 기능

* `1차 캐시`와 `동일성`(같은 트랜잭션 안에서는 같은 엔티티를 반환)을 보장.
* 트랜잭션이 커밋 되기 전까지 쿼리를 모아 `쓰기지연` 가능
* 또한 연관관계 테이블이 `실제 사용될 때 로딩`되도록 `지연 로딩` 가능.

</details>


# Q. SQL Mapper를 사용해본 경험 ?
<details>
	<summary>Questions</summary>

* SQL Mapper를 사용한 이유 ?
* 사용하면서 편리했던 점?
* 불편했던 점?
* 어려웠던 점?

</details>

# Q. ORM을 사용해본 경험 ?
<details>
	<summary>Questions</summary>

* ORM 프레임워크를 사용한 이유 ?
* 사용하면서 편리했던 점?
* 불편했던 점?
* 어려웠던 점?

</details>

# Q. 영속성 컨텍스트 ?
<details>
	<summary>Answer</summary>

* 영속성 컨텍스트란 ?
	* 영속성 컨텍스트란 엔티티를 영구 저장하는 환경을 의미.
	* 영속성 컨텍스는 1차 캐시를 제공해주고, 트랜잭션 내의 Entity의 동일성을 보장해준다. 또한 쓰기지연, DirtyChecking을 통한 유연한 update, 지연로딩을 통해 성능 최적화 기능이 가능하다는 장점을 지닌다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [자바 ORM 표준 JPA 프로그래밍 - 기본편 - 인프런 | 강의](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)


</details>
