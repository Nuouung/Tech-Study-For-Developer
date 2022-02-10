# Data Strucure

## Q. ArrayList와 LinkedList의 차이점

<details>
  <summary>Answer</summary>
  
ArrayList는 순서를 유지하며 데이터를 관리하기 때문에 빠른 조회가 가능하지만, 삽입, 삭제가 느림. 반면 LinkedList는 양방향 연결 리스트 구조로 구성되어 있어 삽입, 삭제가 빠르지만 인덱스를 통한 데이터 접근이 불가능 하기 때문에 조회속도는 느리다는 단점이 존재.
  
</details>
<details>
  <summary>이해하기</summary>

## Reference
- [링크1](https://www.hanbit.co.kr/channel/category/category_view.html?cms_code=CMS4973879534)
- [링크2](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Array%20vs%20ArrayList%20vs%20LinkedList.md)
- [링크3 with Code](https://devlog-wjdrbs96.tistory.com/64)
- [Doubly Linked List](https://opentutorials.org/module/1335/8940)
  
## 내용
![image](https://user-images.githubusercontent.com/26343023/153250402-59f69b24-6d9d-494d-a9a2-c224bbbf7274.png)

### ArrayList

- ArrayList는 배열과 같이 연속적인 메모리 공간에 데이터가 저장되어 있다. 따라서 index를 통한 접근이 가능하다는 장점이 있다.
- 하지만 데이터를 삽입, 삭제 할 때는 순서를 유지하기 위해 추가적인 이동연산이 수행된다.
- [1, 2, 3, 4, 5, 6] 과 같은 데이터가 존재할 때 추가로 7을 삽입하려면 내부적으로 메모리 공간을 증가시키고, 기존의 값을 복사 해서 다시 넣고, 새로운 데이터를 마지막에 추가한다.
- 만약 중간의 3을 삭제하게 되면 3을 지우고, [4, 5, 6]을 한칸씩 땡겨서 빈 공간을 채워줘야 한다.

  
### LinkedList
![image](https://user-images.githubusercontent.com/26343023/153390516-1562e85e-f70f-4385-9a4b-5b65ceb0297a.png)

  
- LinkedList는 양방향 연결 리스트 구조로 되어있다.(자신의 앞, 뒤 노드를 가르키는 링크를 가지고 있다.)
- 따라서 데이터가 추가 된다면 마지막 노드의 next link를 새롭게 추가 된 노드와 연결하고, 새롭게 추가 된 노드의 prev link를 마지막 노드와 연결해주면 끝이다.
- 삭제도 마찬가지로 자신의 앞, 뒤 데이터를 가르키는 Link Filed만 변경해주면 된다.
- 하지만 데이터가 순차적으로 저장되어 있지 않기 때문에, index를 통한 접근이 불가능하다. 따라서 데이터를 찾기 위해서는 첫번째 데이터부터 순차탐색을 해야한다.

</details>

## Q. HashTable 이란?

<details>
  <summary>Answer</summary>
Key와 Value로 데이터를 저장하는 자료구조. HashTable은 Key값에 해시함수를 적용해 고유한 index(주소 값)을 지정할 수 있다. 따라서 한 번의 해쉬함수만을 수행하여 빠르게 데이터를 조회, 삭제, 저장할 수 있다.
  
</details>
<details>
  <summary>정리</summary>

### Reference
- [링크1 - 망나니개발자 블로그](https://mangkyu.tistory.com/102)
- [링크2 - HashTable vs ConcurrentHashMap](https://roynus.tistory.com/672)
- [링크3 - HashTable vs ConcurrentHashMap](https://stackoverflow.com/questions/12646404/concurrenthashmap-and-hashtable-in-java)
  
### 내용
<img width="302" alt="image" src="https://user-images.githubusercontent.com/26343023/153461185-b8809191-d63e-48f6-8484-ec21cf2592ed.png">

### 해시 함수의 결과가 같은 경우?
  
- 이와 같은 경우를 `해시 충돌`이라고 한다.
- 해시 충돌이 발생한 경우 기존의 value를 저장하고 있는 메모리 공간 뒤에 이어 붙여서 해결할 수 있다.
  - 같은 key에 데이터가 연속적으로 저장된다.
  - 해시테이블의 확장이 필요없이 간단하게 구현이 가능하다. 하지만 같은 key에 대한 충돌이 자주발생하면 그만큼 탐색속도가 떨어지게 된다.
  - 이를 `분리 연결법(Separate Chaining)`이라 한다.
- 또는, 해시 테이블의 비어있는 공간에 채워넣는 방법도 있다.
  - 특정 규칙에 따라 테이블의 빈공간을 찾아가면서 값을 저장하게 된다.
  - 이는 `개방 주소법(Open Addressing)` 이라 한다.
  - 개방 주소법으로 저장할 때, 삭제 된 공간은 Dummy Space로 활용되기 때문에 HashTable의 공간을 재정렬 해주는 작업이 필요하다.(클러스터링 작업이 필요하다.)

### 해시테이블 시간복잡도

- 평균 적으로 O(1)의 시간을 가진다.
- 하지만 분리 연결법으로 저장되어 있는 경우, Chaining되어 있는 데이터를 찾아가면서 O(N)까지 속도가 저하될 수 있다.
  
  
### Java에서 HashMap vs HashTable vs ConcurrentHashMap

- HashTable은 Thread-Safe하다, synchronized 키워드를 사용해 멀티 쓰레드 환경에서 안전하게 사용할 수 있다. 반면 HashMap은 동기화에 대한 고려를 하지 않기 때문에, 멀티쓰레드 환경에서 사용할 시 문제가 발생할 수 있다.
- ConcurrentHashMap도 Thread-Safe하다. 
- ConcurrentHashMap과 HashTable는 성능에서 차이가 난다. ConcurrentHashMap이 더 빠르다.
  - HashTable은 synchronized 키워드로 메소드 전체에 락을건다. 즉, HashTable 객체를 참조하는 쓰레드가 많아지면 그만큼 대기시간이 길어질 수 밖에 없다.
  - 반면 ConcurrentHashMap는 내부적으로 여러 개의 세그먼트를 두고 각 세그먼트마다 Lock을 가진다.
    - 때문에 여러 쓰레드에서 ConcurrentHashMap객체에 동시에 데이터를 삽입, 참조하더라도 다른 세그먼트에 위치하면 서로 경쟁하지 않는다.
    - 이런 방법을 Lock Striping이라고 한다. (역역을 나누고, 그 영역마다 다른 락으로 동기화 하는 방법)
 

</details>

## Q. 이진 트리란?

<details>
  <summary>Answer</summary>
</details>
<details>
  <summary>정리</summary>

### Reference
  
### 내용


</details>


## Q. sample?

<details>
  <summary>Answer</summary>
</details>
<details>
  <summary>정리</summary>

### Reference
  
### 내용


</details>

