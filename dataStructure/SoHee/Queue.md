# FIFO(First-In,First-Out)
- 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조를 말한다.
> Queue의 사례
- 너비우선탐색(BFS)
- 캐시(Cache)구현



![](https://images.velog.io/images/dodamtanguri/post/795337ff-03ee-4169-8251-60525542358c/image.png)



[이미지 출처](https://namu.wiki/w/%ED%81%90(%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0))


Java에서 Queue는 java.util 패키지에서 제공

```java
public interface Queue<E> extends Collection<E> {
	boolean add(E e);
    boolean offer(E e);
    E remove();
    E poll();
    E element();
	E peek();
}

```
- Enqueue : 큐에 데이터 넣는 기능
```java
boolean add(E e); //true 또는 예외
boolean offer(E e); //true 또는 false
```
![](https://images.velog.io/images/dodamtanguri/post/884f9136-2c13-47dc-ac59-1cf6115e6cc3/image.png)![](https://images.velog.io/images/dodamtanguri/post/7e4622fa-2c67-4974-bed6-b042d15b6d36/image.png)
- Dequeue : 큐에서 데이터를 꺼내는 기능
```java
E remove(); //첫번째값 반환 또는 null
E poll(); //첫번째값 반환 또는 **NoSuchElementException**
```
- 다음 값 확인
```java
 E element(); // 다음값 또는 null
 E peek(); // 다음값 
```
![](https://images.velog.io/images/dodamtanguri/post/11487d6b-4e03-4be8-a3eb-cd8c09d97eb1/image.png)

### ArrayList를 활용해 Queue구현하기
```java
import java.util.ArrayList;

public class Queue<T> {
	private ArrayList<T> queue = new ArrayList<T>();
    
    public void enQueue(T n) {
    	queue.add(n);
    }
    
    public T deQueue() {
    
    	//queue가 비어있다면 
        if(queue.isEmpty()) {
        	return null;
        }
        
        //list의 가장 앞에 있는 값 제거
        return queue.remove(0);
    }
   
}
```


