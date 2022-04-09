### 

### Persistance
- 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성
- 영속성을 갖지 않는 데이터는 메모리에만 존재하기 때문에 프로그램을 종료하면 모두 잃어버리게 된다.



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
 
