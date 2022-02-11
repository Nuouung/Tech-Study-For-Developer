# ****Data Structure****

---

- 여러 데이터를 효율적으로 관리하기 위한 구조

# ****Linear Data Structure****

---

- 데이터들이 순차적으로 저장되어 있는 구조
- 종류
    - 배열, 리스트 : 인덱스를 통해 원소에 접근
    - 스택, 큐, 디큐 : 제한된 접근(삽입/삭제) 허용
    - 연결 리스트 : 데이터들이 메모리에 연속되지 않게 저장되어 있다. 각 데이터들은 값과 다음 데이터의 주소를 가지고 있다. 인덱스로 접근할 수 없고 처음부터 계속 찾아가야 한다

# Stack

---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3eb6a396-6454-4b86-aa95-b8fe9090ef91/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220211T081509Z&X-Amz-Expires=86400&X-Amz-Signature=b946f5299c7b7fce1f0f9869ab81313782663d1f564af38d6bb975153752e4f5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 한쪽 끝에서만 데이터를 삽입/삭제할 수 있는 자료구조로 가장 마지막에 들어온 데이터가 가장 먼저 나가는 LIFO[ Last In First Out ] 구조 입니다. 재귀 함수, DFS 등에서 사용됩니다.
- Java Stack

    ```java
    // 상속 관계 
    java.lang.Object
    	java.util.AbstractCollection<E>
    		java.util.AbstractList<E>
    			java.util.Vector<E>
    				java.util.Stack<E>
    
    public class Stack<E> extends Vector<E>
    
    // 사용법 
    import java.util.Stack; 
    
    Stack<Integer> stack = new Stack<>();
    ```

    - java.lang.Object : 모든 클래스의 부모 클래스이다. 부모가 없는 클래스도 자동적으로 Object 클래스를 상속 받는다. Object 클래스에 정의되어 있는 메소드들을 통해 클래스의 기본적인 기능을 사용할 수 있다
    - java.util.AbstractCollection<E> : 컬렉션 인터페이스의 뼈대를 제공한다
    - java.util.AbstractList<E> : 리스트를 구현하는데 뼈대를 제공한다. random access하게 데이터를 저장한다.
    - java.util.Vector<E> : 함수들이 synchronzied하게 선언되어 thread safe 하다

- Java Stack 관련 메서드
    - pop(E item) : item 삽입
    - pop() : top item 삭제 후 item 반환
    - peek() : top item 반환
    - empty() : 비어있으면 true, 안비어있으면 false 반환
    - search(Object o) : o의 위치 반환. top 위치는 1이고 o 없으면 -1 반환
- Java 구현 코드

    ```java
    public class MyStack {
    	
    	private static class StackNode {
    		private T data;
    		private StackeNode next;
    		
    		public StackNode(T data) {
    			this.data = data;
    		}
    	}
    	
    	private StackNode top;
    	
    	public T pop() {
    		if(top==null) throw new NoSuchAlgorithmException();
    
    		T item = top.data;
    		top = top.next;
    		return item;
    	}
    	
    	public void push(T item) {
    		StackNode node = new StackNode(item);
    		node.next = top;
    		top = node;
    	}
    	
    	public T peek() {
    		if(top==null) throw new NoSuchAlgorithmException();
    		return top.data;
    	}
    	
    	public boolean isEmpty() {
    		return top==null;
    	}
    
    }
    ```


# Queue

---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a342b2bc-a5e8-4392-b3a1-b74e8471295c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220211T081553Z&X-Amz-Expires=86400&X-Amz-Signature=1f014c04874cd6cd73b5bc1b099a467ceca3c52b65ba88817b902f714d085b68&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 한쪽 끝에서 삽입하고 다른 한쪽 끝에서는 삭제하는 자료 구조로, 먼저 넣은 데이터가 먼저 나오는 FIFO구조입니다. BFS, 캐시, 대기열등에서 사용됩니다.
- Java Queue

    ```java
    Interface Queue<E> extends Collection<E>
    ```

    - Collection 프레임워크의 일부이며 java.util 패키지에 소속되어 있다.
    - interface인 큐를 제네릭 형태로 사용할 때 큐를 구현한 클래스를 사용한다
        - LinkedList
        - PriorityQueue : 우선순위 큐
        - PriorityBlockingQueue : 동기화된 PriorityQueue
- Java Queue 관련 메서드
    - add(item) : 큐 끝 부분에 item 추가
    - remove() : 큐의 첫 번쨰 항목 제거
    - peek() : 큐의 가장  위에 있는 항목 반환
    - isEmpty() : 큐가 비어있을 때 true 반환
- Java Queue 구현

    ```java
    public class MyQueue {
      private static class QueueNode {
        private T data;
        private QueueNode next;
    
        public QueueNode(T data) {
          this.data = data;
        }
      }
    
      private QueueNode first;
      private QueueNode last;
    
      public void add(T item) {
        QueueNode node = new QueueNode(item);
    
        if (last != null) last.next = node ;
        last = node;
        if (first == null) first = last;
      }
    
      public T remove() {
        if (first == null) throw new NoSuchElementException();
        T data = first.data;
        first = first.next;
    
        if (first == null) last = null;
        return data;
      }
    
      public T peek() {
        if (first == null) throw new NoSuchElementException();
        return first.data;
      }
    
      public boolean isEmpty() {
        return first == null;
      }
    }
    ```


# Array

---

- 같은 종류의 데이터를 메모리에 연속적으로 저장해 관리하는 자료구조. 배열의 요소마다 인덱스를 부여해서 이를 통해 빠르게 접근이 가능하며 미리 크기를 지정해야 한다는 특징이 있다. 한 번 생성된 배열의 길이는 변경할 수 없기 때문에 저장할 공간이 부족할 경우 더 큰 길이의 배열을 생성한 후 기존 배열의 값을 복사해야 한다.
- 중간에 데이터를 삭제해도 빈 공간인채로 남겨둬야해서 메모리가 낭비된다.

# List

---

- 빈틈없이 순서대로 데이터를 적재하는 자료 구조
- 동적이므로 크기가 정해져 있지 않고 포인터를 통해 다음 데이터의 위치를 가리키고 있어 삽입/삭제가 용이 하다.
- 검색 성능이 좋지 않고 포인터를 이용하므로 추가적인 메모리 공간이 필요하다

# ArrayList

---

- 인덱스로 객체를 관리한다는 점에서 Array와 동일하지만, 크기를 동적으로 늘릴 수 있다는 차이점이 있다.
- 내부에서 배열을 사용하기 때문에 인덱스를 이용해 빠르게 조회가 가능하지만 추가/삭제는 느리다.
    - 추가 : 처음이나 중간에 데이터를 추가하면 이후 데이터들을 1칸씩 뒤로 미뤄야 한다.
    - 삭제 : 처음이나 중간에 데이터를 삭제하면 이후 데이터들을 1칸씩 앞으로 당겨야 한다.
- 객체를 선언할 때 매개변수를 넣지 않으면 초기 크기는 10으로 할당된다. 만약 기존 용량이 꽉 찼을 경우, 기존 용량의 1.5배를 늘린 새로운 배열을 만들어 기존 배열을 copy하는 작업이 내부에서 자동으로 수행된다.
- Java ArrayList

    ```java
    java.lang.Object
    	java.util.AbstractCollection<E>
    		java.util.AbstractList<E>
    			java.util.ArrayList<E>
    
    public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, Serializable
    ```


# LinkedList

---

- List와 Queue 인터페이스를 구현한 클래스
- 노드간 연결을 통해 리스트로 구현된 객체
- 인덱스를 가지고 있지 않기 때문에 순차 접근만 가능하며 삽입/삭제 성능이 좋다
    - 삽입 과정
        1. 추가될 자료의 node를 생성한다
        2. 추가될 node의 이전 node의 다음 node를 추가될 node로 설정한다
        3. 추가될 node의 다음 node를 이전 node의 다음 node로 설정한다
    - 삭제 과정
        1. 삭제할 node의 이전 node의 다음 node를 삭제할 node의 다음 node로 설정한다
- 각 데이터를 앞 뒤로 연결하는 구조이기 때문에 미리 공간을 할당해 놓을 필요가 없다

# Array vs ArrayList

---

- Array는 초기화시 메모리에 할당되어 속도가 빠르고 다차원 배열이 가능하다. 하지만 사이즈가 고정되어 있어서 변경할 수 없다. 그렇기 때문에 데이터의 크기가 얼마나 되는지 아는 경우는 Array를 사용하고, 그렇지 않다면 ArrayList를 사용한다. ArrayList는 Array보다 속도가 느리지만 사이즈를 고정하지 않아도 되며 동적으로 값의 추가/삭제가 가능하다.
- 배열은 크기가 고정되어 있지만 arraylist는 크기가 동적인 배열이다.
- 배열은 primitive type(int, byte, char 등)과 object 모두를 담을 수 있지만, arrayList는 object element만 담을 수 있다
- 배열은 제네릭을 사용할 수 없지만, arrayList는 타입 안정성을 보장해주는 제네릭을 사용할 수 있다

# ArrayList vs LinkedList

---

- 데이터를 조회하는 경우

  ArrayList는 인덱스 기반의 자료구조이기 때문에 데이터를 찾을 때 O(1) 시간 복잡도를 가진다. 반면에 LinkedList는 첫번째 노드부터 순서대로 탐색해야 하기 때문에 최악의 경우 O(n) 시간이 걸린다.

- 데이터를 중간에 추가/삭제 하는 경우

  ArrayList는 중간에 데이터를 추가/삭제하면 뒤에 있는 데이터들을 복사 후 다시 재배치 해야 해서 최악의 경우 O(n) 시간이 걸린다. LinkedList는 이전 노드와 다음 노드의 참조 상태만 변경하면되서 O(1) 시간 복잡도가 걸린다.

- 데이터를 마지막에서부터 삭제하는 경우

  ArrayList는 재배치가 필요하지 않아 O(1)  시간이 걸리고 LinkedList는 마지막 노드까지 매번 접근해야 하므로 O(n) 시간 복잡도가 걸린다

- 데이터 접근이 중요하다면 ArrayList를 사용하고, 데이터 추가/삭제가 빈번하다면 LinkedList를 사용하는게 좋다.

# ArrayList vs Queue

---

- 큐는 한쪽에서 삽입이 이뤄지고 다른 한쪽에서 삭제가 이루어 지지만 ArrayList는 위치와 상관없이 데이터를 추가/삭제가 가능하다

# Non-****Linear Data Structure****

---

- 데이터들이 계층적으로 저장되는 구조
- 예시
    - 트리
    - 그래프

# Graph

---

- 노드와 간선으로 이루어진 자료 구조
- 노드들 사이에는 무방향/방향/양방향 경로를 가질 수 있다
- 순환 혹은 비순환 구조이다.
- 종류
    - 방향 그래프 : 그래프에 방향이 존재
    - 무방향 그래프 : 그래프에 방향이 존재하지 않아 양 방향으로 갈 수 있는 그래프
    - 가중치 그래프 : 간선에 가중치가 할당된 그래프

# Tree

---

- 그래프의 일종으로 노드들을 계층적으로 연결해서 사용하는 비선형 자료 구조
- 관련 용어
    - 루트 노트 : 맨 위에 위치한 노드
    - 리프 노트 : 자식이 없는 노드
    - 서브 트리 : 트리에서 어떤 한 노드와 그 노드의 자손들로 이루어진 트리
    - 간선/엣지/링크/브랜치 : 노드와 노드를 연결한 선
    - 높이 : 트리에 존재하는 서로 다른 레벨의 총 개수
    - 깊이 : 루트 노드부터 현재 노드까지 오는 데 거치는 간선의 개수
- 순회 방법
    - 전위 순회 [pre-order] : 루트 - LEFT - RIGHT
    - 중위 순회 [in-order] : LEFT - 루트  - RIGHT
    - 후위 순회 [pre-order] : LEFT - RIGHT - 루트  or RIGHT - LEFT - 현재 노드
    - 레벨 순회 : 형재 노드들을 모두 방문한 후 하위 노드를 탐색
- 트리 종류
    - 이진 트리
        - 각 노드가 최대 2개의 자식을 가지는 트리
        - 종류
            - 완전 이진 트리 : 루트 노드 부터 시작해 왼쪽에서 오른쪽으로 모든 노드가 차 있는 상태
            - 포화 이진 트리 : 리프노드가 있는 층위까지 모든 노드들이 꽉 차있는 상태
    - 이진 탐색 트리
        - 중복된 값이 없으며 왼쪽 자식 노드 값 < 루트 노드 값 < 오른쪽 자식 노드 값 을 만족하는 이진 트리

# Heap

---

- 완전 이진 트리의 일종으로 우선 순위 큐를 위해 만들어진 자료 구조
    - 우선 순위 큐 : 우선순위를 가진 데이터들이 있고 우선순위가 높은 데이터가 먼저 나간다는 개념을 큐에 도입한 자료 구조
- 최대값/최소값을 빠르게 찾아내도록 만들어진 자료 구조
- 종류
    - 최소 힙 : 부모 노드의 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
    - 최대 힙 : 부모 노드의 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리

# **Collection Framework**

---

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/113303fb-8722-44ad-bc03-dde89e670918/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220211T081625Z&X-Amz-Expires=86400&X-Amz-Signature=28a7f3cd67aa5f335634dc3f3a0bb6e6c2ffaac2920c370a8b59449b6125381b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- 다양한 자료 구조들을 구조화해서 제공한다
- 자료구조의 주요 기능들이 collection 인터페이스에 정의되어 있다