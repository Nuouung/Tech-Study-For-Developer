#  Q. 트랜잭션과 트랜잭션이 지닌 특성에대해 설명하시오
<details>
	<summary>Answer</summary>
  
* DB에서 트랜 잭션이란 하나의 작업을 처리하기 위한 단위이며,  ACID 4가지 특성을 지니고 있습니다.
	* 원자성(Atomicity)
	* 일관성(Consistency)
	* 격리성(Isolation)
	* 영속성(Durability)

* 원자성은 All or Nothing을 의미. 하나의 트랜잭션은 완벽하게 실행되거나, 처리 중 문제가 발생하면 모두 취소되어야 한다.

* 일관성은 시스템이 가지고 있는 고정 요소는 트랜잭션 수행 전, 후가 같아야 함을 의미.

* 격리성이란 하나의 트랙잭션이 실행되는 도중에는 다른 트랜잭션이 끼어들 수 없음.

* 영속성이란 트랜잭션이 성공적으로 완료되었다면, 그 결과는 영구적으로 보존되어야 함을 의미.


</details>

<details>
	<summary>이해하기</summary>

## Reference
* [YouTube](https://www.youtube.com/watch?v=q_KU7Ek_XA4&ab_channel=%EC%97%90%EB%93%80%EC%98%A8)
  
## 내용
* 일관성
	* 만약 A가 1000원, B가 0원이 있을 때
	* A가 B에게 500원을 보내면 각각 500원씩 잔액이 남아있어야 한다.
	* 만약 A는 500원이 차감되었지만, B는 추가되지않고 0원에 머물러있다면? 일관성이 깨진것이다.

* 영속성
	* 어떠한 천재지변이 발생할지라도 트랜잭션이 성공한 데이터는 사라지거나 변경되면 안된다.

</details>


# Q. 격리 수준

<details>
	<summary>Answer</summary>
  
* 트랜잭션의 독립성은, 실행중인 트랜잭션에 끼어들 수 없음을 의미한다. DB에서는 다른 트랜잭션에 접근할 수 있는 수준을 4단계로 나누어 구분하고 있다.
  * 단계가 내려갈수록  격리 수준은 높아지지만, 성능은 떨어진다.
  * 단계가 내려갈수록 동시성은 떨어지지만, 데이터 정합성은 높아진다.

1. READ-UNCOMMITED
* `commit 전`의 트랜잭션 데이터 변경 내용을 다른 트랜잭션이 읽을 수 있다. 
* 하지만 이 경우 커밋 이전에 참조한 데이터가 rollback될 수 있다. 
* 즉, `Dirty Read가 발생`할 수 있다.

2. READ-COMMITED
* READ-UNCOMMITTED 의 `Dirty Read문제를 해결`한다. 
* `커밋이 완료된 트랜잭션`의 변경사항만 다른 트랜잭션에서 조회할 수 있다.  
* `대부분 RDB는 READ-COMMITED가 Default` 값이다.
* READ-COMMITED는 동일한 쿼리의 결과가 다른결과를 출력하는 `Non-Repeatable Read문제가 발생`할 수 있다. 
* 즉, 데이터가 불일치하는 문제가 발생한다. 

3. REPEATABLE-READ
* READ-COMMITED와 같이 커밋이 완료된 트랜잭션만 참조가 가능하다.
* 하지만 Non-Repeatable Read문제를 해결하여 `한 트랜잭션에서 동일한 요청에 같은 결과를 출력`한다.
* REPEATABLE-READ에서는 `실행결과 갯수가 달라지는 Phantom Read 문제가 발생`할 수 있다.
	* 하나의 트랜잭션에서 `count(*)에 대한 결과 개수가 다르다.`
	* 중간에 다른트랜잭션에서 데이터가 추가된다면 결과가 달라질 수 있다.

4. SERIALIZABLE
* `다른 트랜잭션으로의 접근이 불가`하다.
* 가장 엄격하지만 성능은 가장떨어진다.
* 데이터 베이스에서는 `잘 사용되지 않는다.`

</details>

<details>
	<summary>이해하기</summary>

## Reference
*  [nesoy.github.io](https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation) 
*  [우아한Tech](https://www.youtube.com/watch?v=e9PC0sroCzc&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9CTech) 

</details>

# Q. DB의 무결성(정확성)을 유지하기 위한 제약조건
<details>
	<summary>Answer</summary>

1. 개체 무결성 제약조건
* 기본키에 대한 성질을 의미한다.
* `기본키는 NULL이나 중복값을 가질 수 없다.`

2. 참조 무결성 제약조건
* `참조할 수 없는 외래키 값을 가질 수 없다.`
* 즉, 외래키로 찾아갔는데 데이터가 존재하지 않는다면 참조 무결성을 위배한 것.

3. 도메인 무결성 제약조건
* 주어진 속성의 값이 도메인에 속한 값이어야 한다.
	* 도메인이란 속성이 가질 수 있는 값의 범위를 의미한다. 
	* ex) 성별은 남, 여의 값을 가진다.
* 즉, `도메인을 벗어나는 값이 입력되면 안된다.`
	* 성별에는 남, 여만 입력되어야 한다.

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [YouTube](https://www.youtube.com/watch?v=K3YxdmHj4sg&ab_channel=%EC%97%90%EB%93%80%EC%98%A8)
 
</details>

# Q. DB 정규화의 목적과 과정

<details>
	<summary>Answer</summary>

## 목적
* 데이터 구조의 안정성을 최대화
* `중복을 배제하여 삽입, 삭제, 갱신 이상의 발생을 방지.`

## 정규화 과정
* 1 정규형 -> 2 -> 3 -> BCNF -> 4 -> 5 정규형
	* 도부이결다조
* 실무에서는 대부분 1~3, 필요시 BCNF까지 정규화 과정을 거침.

### 1 정규형
* 모든 도메인은 원자값을 갖도록 해야한다.
	* DB에서 원자값이란 모호한 개념이다.
	* ex) 홍길동이라는 이름은 성(홍)과 이름(길동)을 나눌 수 있다.

* 1정규형은, 여러개의 주제를 갖는 속성 값들을, 하나의 주제를 갖는 테이블이 될 수 있도록 분해하는 것.

### 2 정규형
* 부분 함수적 종속을 제거한다. 
	* 부분함수적 종속은 복합키를 가진 테이블에서 발생한다.
	* `학번, 주민등록번호`로 복합키가 구성되어 있다면
	* `주민등록번호`만으로도 학생의 이름을 알 수 있다.
	* 이러한 경우를 부분함수 종속이 발생했다고 표현하며, `주민등록번호`를 key로 가지는 새로운 테이블로 생성하여 분리한다.
		* 주민등록 번호를 PK로 하는 경우는 드물지만 직관적으로 표현하고자 예시로 들었다.


### 3 정규형
* 이행적 함수적 종속제거
	* A -> B -> C 의 관계가 존재해서는 안된다.
	* `주문번호(pk), 주문날짜, 회원ID, 회원명, 회원등급` 로 테이블이 구성되어있다면
		* 주문번호(A)로는 회원 ID(B)가 결정된다. (누가 주문했는지 알아야하니까)
		* 회원 ID(B)로는 회원명(C), 회원등급(C)이 결정된다.
	* 이 경우 `주문번호(pk), 주문날짜, 회원ID`
	* `회원ID(pk), 회원명, 회원등급`
	* 2개의 테이블로 분리한다.

### BCNF
* 모든 결정자는 후보키어야 한다. 후보키가 아닌속성이 결정자가 되면 안된다.
* 많이 발생하지 않는다.

### 4 정규형
* 다치 종속제거
* 다치종속(MVD)
* Multi Value

### 5 정규형
* 조인종속 제거

</details>

<details>
	<summary>이해하기</summary>

## Reference
* [YouTube](https://www.youtube.com/watch?v=RXQ1kZ_JHqg&ab_channel=%EC%97%90%EB%93%80%EC%98%A8)
  
</details>

# Q. Clustered Index vs Non Clustered Index
<details>
	<summary>Answer</summary>


## Clustered Index
* 테이블 당 1개만 생성 가능하다.
* 물리적으로 정렬되어 있다.
	* Leaf노드에 실제 데이터가 존재한다.
* PK설정 시 자동으로 클러스터드 인덱스가 생성된다.
	* 즉, `해당 테이블은 PK를 기준으로 정렬되어 저장`된다.
	* PK로 자동생성되는것을 원하는 컬럼으로 변경하는것도 가능하다.(복합키도 가능)
* 검색속도는 빠르지만 삽입, 수정, 삭제는 느리다.
	* 정렬을 유지해야하기 때문에 이동연산이 수행된다.
* 테이블이 자주 변경되지 않고, 자주 조회하는 경우에 유리하다.
	* 범위검색을 할 때도 좋다. (빠르게 Leaf 노드에 도달이 가능하니깐)


## Non Clustered Index

* 인덱스를 충분히 생성할 수 있다. (249개?)
* `별도의 디스크 공간에 인덱스 테이블을 생성`한다.
* 따라서 Leaf노드에는 데이터가아닌, 데이터에 대한 포인터가 존재한다.
	* 실제 데이터가 존재하는 테이블에 대한 포인터(주소 값)
* Leaf노드의 구조는 마치 LinkedList와 유사하다. 즉, 논리적(물리적 x)으로 연결되어있기 때문에 조회속도는 느리지만 삽입, 삭제, 변경의 속도는 빠르다.


</details>

<details>
	<summary>이해하기</summary>

## Reference

* [탁구치는 개발자 :: 클러스터드 인덱스와 넌 클러스터드 인덱스](https://lng1982.tistory.com/144)
* [데이터베이스 클러스터 인덱스와 넌클러스터 인덱스/ 개념 총정리](https://junghn.tistory.com/entry/DB-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0-%EC%9D%B8%EB%8D%B1%EC%8A%A4%EC%99%80-%EB%84%8C%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0-%EC%9D%B8%EB%8D%B1%EC%8A%A4-%EA%B0%9C%EB%85%90-%EC%B4%9D%EC%A0%95%EB%A6%AC)
* https://gocoder.tistory.com/1826
* https://gwang920.github.io/database/clusterednonclustered/

  
## 내용

### 인덱스란?
* 정렬된 컬럼을 별도의 디스크에 저장하여 색인의 역할을 해주어 빠른 검색을 도와주는 역할을 한다.
* 인덱스는 별도의 디스크 공간이 필요하고, 인덱스를 가진 테이블에 DML을 수행하는 경우 더 많은 비용과 시간이 필요.
* 따라서 인덱스를 생성시 Clustered, Non Clustered 인덱스를 구분하여 생성하는 것은 중요한 개념

</details>

# Q. SQL DB VS NoSQL DB
<details>
	<summary>Answer</summary>

SQL DB는 스키마를 통해 구조적인 데이터를 저장하기 때문에, 데이터 무결성을 보장하고 중복없이 데이터를 저장할 수 있습니다.

반면 NoSQL은 스키마가 존재하지 않아 더욱 유연하게 데이터를 저장할 수 있지만, 중복이 발생할 수 있고, 중복 데이터가 수정되면 모든 컬렉션에서 수행되어야 한다는 단점이 있습니다.

NoSQL은 Scale Out(수평적 확장)이 가능하다는 장점을 지니며, HashMap구조로 저장되어 SQL DB보다 빠른 조회속도를 가집니다.

SQL DB는 데이터간의 관계가 존재하고, 데이터의 변경이 자주 일어나는 경우에 사용하는 것이 좋고, NoSQL DB는 데이터 구조가 명확하지 않고, 변경이 적고 읽기 처리를 자주 하는 경우 좋습니다.


</details>

<details>
	<summary>이해하기</summary>

## Reference
* [SQL vs NoSQL (MySQL vs. MongoDB)](https://siyoon210.tistory.com/130)
* [SQL과 NOSQL의 차이 | 👨🏻‍💻 Tech Interview](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)

  
## 내용


</details>
