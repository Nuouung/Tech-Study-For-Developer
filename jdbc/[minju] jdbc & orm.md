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
