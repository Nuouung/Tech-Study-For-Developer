## 1. 세마포어(Semaphore)와 뮤텍스(Mutex)의 차이
뮤텍스(Mutex)는 Lock과 Unlock개념을 사용하는 이진 세마포어(Binary Semaphore)로 세마포어의 일종입니다.
하지만 critical section에 접근할 수 있는 프로세스 혹은 스레드의 수에 차이가 있습니다.
뮤텍스는 오직 1개의 프로세스 혹은 스레드만이 critical section에 접근할 수 있고, 세마포어는 지정된 변수의 값만큼 접근할 수 있습니다.
또한 뮤텍스는 Locking 매커니즘으로 락을 걸은 쓰레드만이 critical section을 나갈 때 락을 해제할 수 있지만 세마포어는 Signaling 메커니즘으로 락을 걸지 않은 쓰레드도 signal 함수를 사용해 락을 해제할 수 있습니다.

