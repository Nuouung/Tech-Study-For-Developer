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

## Q. Hash 란?

<details>
  <summary>Answer</summary>
</details>
<details>
  <summary>정리</summary>

### Reference
  
### 내용


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

