 ### 0. Persistance
- 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성
- 영속성을 갖지 않는 데이터는 메모리에만 존재하기 때문에 프로그램을 종료하면 모두 잃어버리게 된다.

---
### 1. JDBC (Java Database Connectivity)
#### 1-1. JDBC API
JDBC API : JAVA진영의 Database 연결 표준 인터페이스로 DriverManager가 JDBC API를 구현하여 DB에 접근한다.

- 사용방법 

    1. Class.forName() 메소드를 이용하여 드라이버 로드
    2. DriverManager.getConnection() 을 이용하여 데이터베이스 연결
    3. SQL을 실행하는 객체인 Statement 준비
    4. Statement를 이용하여 ResultSet 얻기

 DB연결, 예외처리 등 개발자가 신경써야하는 것이 많다는 담점이 있다. 이러한 문제를 개선하기 위해 Persistence Framework가 등장했다.
 이를 추상화시켜 제공하는 방식에 따라 SQL Mapper, ORM으로 나눌 수 있다. 이들 모두 내부적으로는 jdbc를 통해 DB에 접근한다.

---
### 2. SQL Mapper
- SQL과 Object를 매핑하는 역할을 한다.
- SQL문의 질의 결과와 객체를 매핑시켜주기 때문에 SQL의존적이고 ORM과는 다른 기술이라고 할 수 있다.

#### 2-1. MyBatis
SQL을 xml파일로 분리하여 관리하고, SQL결과와 객체 인스턴스의 매핑을 도와주는 역할을 수행한다. 테이블 필드가 변경되면 관련된 코드들을 수정해야 하는 것과 사용하는 쿼리 문법이나 데이터 타입에 따라 특정 DBMS에 종속될 수 있다는 단점이 있다. 

**코드상으로 SQL과 JDBC API를 분리했지만, 논리적으로는 아직 강한 의존성을 가지고 있다.**


#### 2-2. Spring JDBC

JDBC의 모든 저수준 처리를 스프링 프레임워크에 위임하므로써, Connection 연결 객체 생성 및 종료, Statement 준비/실행 및 종료, ResultSet 처리 및 종료, 예외 처리, 트랙잭션 등의 반복되는 처리를 개발자가 직접하지 않고 Database에 대한 작업을 수행할 수있다.

---
### 3. ORM
- DB 데이터와 Object를 매핑하는 역할을 한다.
- Object를 통해 간접적으로 DB를 다룬다. (객체와 관계형DB를 자동으로 매핑해 준다.)
- 객체간의 관계를 바탕으로 SQL을 자동으로 생성해 준다.

- 장점 

    1. 별도의 SQL문을 사용하지 않아도 객체 지향 프로그래밍 언어로 구현이 가능하며 이는 곧 생산성 증가로 이어진다.
    2. 재사용 및 유지보수가 편리하다.
    3. DBMS에 대한 종속성이 줄어든다.

- 단점 

    1. DB와 바로 연결하는 것보다 초기설정이 더 많아지거나 복잡해 질 수있다.
    2. 모든 것을 ORM을 통해서만 구현하는 것은 힘들다.
---
### 4. 영속성 컨텍스트
영속성 컨텐스트란 엔티티를 영구 저장하는 환경이라는 뜻이다. 애플리케이션과 데이터베이스 사이에서 객체를 보관하는 가상의 데이터베이스 같은 역할을 한다. 엔티티 매니저를 통해 엔티티를 저장하거나 조회하면 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.
EntityManager가 생성되면 1:1로 영속성 컨텍스트가 생성된다.
EntityManager를 통해서 영속성 컨텍스트에 접근하고 관리할 수 있다.

- 엔티티의 생명주기

    비영속(new/transient): 객체를 생성만 한 상태로 영속성 컨텍스트와 전혀 관계가 없는 상태이다.
    ```java
    Member member = new Member();
    ```
    영속(managed): 영속성 컨텍스트에 저장되어 관리되는 상태이다.
    ```java
    em.persist(member);
    ```
    준영속(detached): 영속성 컨텍스트에 저장되었다가 분리된 상태이다.
    ```java
    // 엔티티를 영속성 컨텍스트에서 분리해 준영속 상태로 만든다.
    em.detach(member);
    // 영속성 콘텍스트를 비워도 관리되던 엔티티는 준영속 상태가 된다.
    em.claer();
    // 영속성 콘텍스트를 종료해도 관리되던 엔티티는 준영속 상태가 된다.
    em.close();
    ``` 
    삭제(removed): 실제 DB 삭제를 요청한 상태이다.
    ```java
    em.remove(member);
    ```

### 영속성 컨텍스트의 특징(장점)

#### 1. 1차 캐시
영속성 컨텍스트 내부에는 캐시가 있는데 이를 1차 캐시라고 한다. 영속 상태의 엔티티를 이곳에 저장한다. 1차 캐시의 키는 식별자 값(데이터베이스의 기본 키)이고 값은 엔티티 인스턴스이다. 
```java
// em.find(엔티티 클래스 타입, 식별자 값);
Member member = em.find(Member.class, "member1");
```

#### 2. 동일성 보장
영속 엔티티의 동일성을 보장한다.
```java
Member a = entityManager.find(Member.class, "member1");
Member b = entityManager.find(Member.class, "member1");
System.out.println(a == b); // 동일성 비교 true
```

#### 3. 쓰기 지연
1차 캐시에 저장하는 동시에 쓰기 지연 SQL 저장소에 저장해두고 commit 실행 시 DB에 쿼리를 한번에 보낸다.
```java
entityManager.persist(memberA);
entityManager.persist(memberB);
// 이때까지 INSERT SQL을 DB에 보내지 않는다.

// 커밋하는 순간 DB에 INSERT SQL을 보낸다.
transaction.commit(); // Transaction 커밋 
```

#### 4. 변경 감지
commit이 호출될 때 현재 엔티티와 캐시 내의 스냅샷을 비교한다. 비교 결과, 변경이 있을 때 수정 쿼리를 생성해서 수정한다.
변경 감지는 영속성 컨텍스트가 관리하는 영속 상태의 엔티티만 적용된다.

#### 5. 지연 로딩
프록시 객체를 이용하여 엔티티가 사용되기 전까지 DB 조회를 지연한다.
