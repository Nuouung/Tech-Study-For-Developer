## Stack (스택)

<div>

**stack**

</div>

  - <span><span data-type="ore" data-lang="en">1</span>.</span><span style="color: #6881a1;">명사</span><span> </span>(보통
    깔끔하게 정돈된) 무더기\[더미\]
    (→<span><span data-type="ore" data-lang="en">haystack</span></span>)
  - <span><span data-type="ore" data-lang="en">2</span>.</span><span style="color: #6881a1;">명사</span><span> </span><span style="color: #888888;">비격식
    특히 英<span> </span></span>많음, 다량

<!-- end list -->

  - <span><span data-type="ore" data-lang="en">3</span>.</span><span style="color: #6881a1;">동사</span><span> </span>(깔끔하게
    정돈하여) 쌓다\[포개다\]; 쌓이다, 포개지다
  - <span><span data-type="ore" data-lang="en">4</span>.</span><span style="color: #6881a1;">동사</span><span> </span>(어떤
    곳에 물건을 쌓아서) 채우다

 

사전에 stack을 검색해보면 저런 결과를 얻을 수 있다. '보통 깔끔하게 정돈된 무더기'.

사전의 뜻처럼 자료구조상의 stack은 책을 쌓듯 차곡차곡 쌓아 올린 형태의 자료구조를 말한다.

 

\[\#\#\_Image|kage@uvu71/btrsSvxJweN/gTTYe95HRFejIchykaxlbk/img.png|CDM|1.3|{"originWidth":1024,"originHeight":736,"style":"alignCenter","width":430,"height":309,"caption":"https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%83%9D","filename":"stack.png"}\_\#\#\]

####  

#### **stack의 특징**

스택을 가장 잘 표현하는 표현은 LIFO로 Last In First Out의 약자이다. 즉, 나중에 들어간 것이 먼저 나오는
자료구조를 스택이라고 표현할 수 있다. LIFO를 한국어로는 후입선출이라고 한다.

 

한번 생각해보자. 책을 바닥에 차곡차곡 무더기로 쌓아 놓은 장면을. 무더기의 가장 위쪽의 책을 꺼내는 것은 어렵지 않지만 가장
아래쪽의 책을 꺼내는 것은 어렵지 않은가. <span style="color: #9d9d9d;">(위의 그림을 책으로 보고
생각해 보아도 무방할 것 같다.)</span>

 

책을 바닥에 쌓아두는 비유는 스택을 이해하는데 도움이 되기는 하지만 완벽하지는 않은 것 같다.
<span style="color: #9d9d9d;">(위에 놓여 있는 책을 조금씩 밀어내며 아래 책을 뺄 수 있기
때문에\!)</span> 그렇다면 항아리에 차곡차곡 쌓여 있는 김치를 떠올려보자. 가장 아래쪽에 있는 김치가 가장
나중에 꺼내질 김치라는 것을 쉽게 상상할 수 있을 것이다.

 

앞서 말한바와 같이 스택은 선형 구조(LIFO)로 되어 있다. 스택에 데이터를 넣는 것을 **push**, 들어 있는 데이터를
꺼내는 것을 **pop**이라고 한다.

 

만약 스택의 크기보다 많은 데이터가 들어갈 경우 데이터는 더 이상 스택에 들어가지 못하고 넘치게 된다. 이는 스택상에 머물러야
하는 데이터가 다른 메모리 영역을 침범하게 되는 불상사로 이어질 수 있기 때문에 많은 프로그래밍 언어에서는 이를 컴파일
단계에서 예측하고 예외를 발생시킨다. 이 예외의 이름이 바로 그 유명한 stack overflow.
<span style="color: #9d9d9d;">(말 그대로 스택이 넘친다는 뜻)</span>

 

 

 

 

## Queue (큐)

<div>

**queue**<span> </span>

</div>

  - <span><span data-type="ore" data-lang="en">1</span>.</span><span style="color: #6881a1;">명사</span><span> </span><span style="color: #888888;">英<span> </span></span>(무엇을
    기다리는 사람자동차 등의) 줄
  - <span><span data-type="ore" data-lang="en">2</span>.</span><span style="color: #6881a1;">명사</span><span> </span><span style="color: #888888;">컴퓨터<span> </span></span>큐,
    대기 행렬

<!-- end list -->

  - <span><span data-type="ore" data-lang="en">3</span>.</span><span style="color: #6881a1;">동사</span><span> </span><span style="color: #888888;">英<span> </span></span>줄을
    서서 기다리다
  - <span><span data-type="ore" data-lang="en">4</span>.</span><span style="color: #6881a1;">동사</span><span> </span><span style="color: #888888;">컴퓨터<span> </span></span>(수행할
    업무들이) 대기 행렬을 만들다\[이루다\]

 

queue도 stack처럼 매우 직관적인 이름을 가지고 있다. '줄을 서서 기다리다'

사전의 뜻처럼 자료구조상의 queue는 마치 사람들이 줄을 서서 기다린 듯한 형태의 자료구조를 의미한다.

 

\[\#\#\_Image|kage@ok1Er/btrsMec1UYY/xEKAmbLKjvShRfZKuqjhAK/img.png|CDM|1.3|{"originWidth":2000,"originHeight":1309,"style":"alignCenter","width":430,"height":281,"caption":"https://namu.wiki/w/%ED%81%90(%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0)","filename":"b7785ff70f623fedbcae126015a3ae0a18b2f3a785bdd691d803aad2b10aee91f7b3fc438aadd3676cb84b9608ac18c4ce4dcc9a35eed34a61a2ffffff9b56ebae203b4dbe4bf8d8be10e33abea1cdab0983fe92dc2c795396b92509b8531e56.png"}\_\#\#\]

#### **queue의 특징**

큐를 가장 잘 표현하는 표현은 FIFO(First In First Out)으로 먼저 들어간 것이 먼저 나온다는 뜻을 가지고 있다.
FIFO라는 단어의 뜻처럼, 줄을 선 사람들의 행렬처럼 먼저 들어간 것이 먼저 나간다. FIFO는 한국어로 선납선출이라고 한다.
<span style="color: #9d9d9d;">(생각해보면 가장 나중에 줄을 선 사람이 가장 먼저 들어가면 되게 이상할 것
같다.)</span>

 

큐상에서 데이터가 들어오는 위치는 **Rear** 혹은 **Back**이라 표현하는 가장 뒤, 데이터가 나가는 위치는
**Front**라고 표현하는 가장 앞이다. 큐는 우선순위가 높은 것이 먼저 나간다는 우선순위 큐, 큐를 선형(Linear)이
아니라 원형으로 만든 원형 큐 등의 변형이 존재한다. <span style="color: #9d9d9d;">(우선순위큐는
VIP 제도가 있는 대기열 라인, 원형큐는 대기라인 수의 제한이 있는 대기열 라인이라고 생각하면 될 것 같다.) </span>

 

<span style="color: #000000;">큐에 데이터를 넣는 행위를 **Enqueue**, 데이터를 꺼내는 행위를
**Dequeue**라고 한다.</span>

 

 

 

 

 

## Tree (트리)

트리는 노드(Node)로 이루어진 자료구조이다. 앞서 설명한 stack, queue가 선형 자료구조였던 것과는 달리 트리는 비선형
자료구조로 일종의 계층 구조를 가지고 있다. 트리의 주목적은 탐색이며 이를 위해 다양한 종류의 트리가 존재한다. 만약 특정
그래프가 1개 이상의 노드를 가지고 있다면 그 그래프는 트리라 정의할 수 있다. 트리는 루트라고 불리는 특별한
최상위 노드에서 시작되며 각각의 노드는 0개 이상의 자식 노드를 가질 수 있다. 컴퓨터 공학의 자료구조에서 주로 관심을
갖는 트리는 최대 2개의 자식 노드를 가질 수 있는 이진 트리(binary tree)이다.

 

\[\#\#\_Image|kage@cQvB1b/btrsSbTTogp/W2ZPLoD8TP3Vr6Tw4i4Pr0/tfile.svg|CDM|1.3|{"originWidth":300,"originHeight":250,"style":"alignCenter","width":340,"height":283,"caption":"https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%A6%AC\_%EA%B5%AC%EC%A1%B0","filename":"트리.svg"}\_\#\#\]

 

#### **tree의 특징**

트리를 볼 때는 위와 같은 그림으로 주로 나온다. 트리를 볼 때는 최상위 노드, 즉 루트가 아래로 되어 있는 나무 모양을 떠올리면
된다. 실제로 트리에서 각 노드를 부르는 호칭 중, 최상위 노드는 루트(root, 뿌리), 최하단 노드는 리프(leaf,
나뭇잎)라고 한다. <span style="color: #9d9d9d;">(위의 그림의 경우 루트는 2, 리프는
5, 11, 4이다)</span>

 

 

#### **추가적인 tree 학습을 위한 유튜브 영상**

<https://www.youtube.com/watch?v=LnxEBW29DOw> 

 

 

 

 

 

## Heap (힙)

힙은 완전 이진 트리의 일종으로 데이터를 빠르게 꺼내고 삽입할 수 있게 고안되었다. 노드가 가장 큰 값을 가지는 최대 힙(Max
Heap), 노드가 가장 작은 값을 가지는 최소 힙(Min Heap)이 존재하며 두 힙은 구현 목적에 따른 차이가 있을 뿐 완전히
같은 원리를 가지고 있다. 힙은 완전 이진 트리이기 때문에 데이터가 위에서 아래로, 왼쪽에서 오른쪽으로 채워진다.

<span style="color: #ef5369;">아래의 그림은 최대 힙이다.</span>

 

**Max Heap**

  - 최상위 노드(루트)가 가장 큰 값을 가진다.
  - 부모 노드의 값은 항상 자식 노드의 값보다 크다.
  - 노드의 값은 부모 자식 관계에만 성립되며, 형제 사이에는 대소관계가 정해지지 않는다.

 

**Min Heap**

  - 최상위 노드(루트)가 가장 작은 값을 가진다.
  - 부모 노드의 값은 항상 자식 노드의 값보다 작다.
  - 노드의 값은 부모 자식 관계에만 성립되며, 형제 사이에는 대소관계가 정해지지 않는다.

 

\[\#\#\_Image|kage@bQBUNB/btrsMz2QUZd/MS4lYEJLHkNxAXKzZW8da0/img.png|CDM|1.3|{"originWidth":800,"originHeight":960,"style":"alignCenter","width":400,"height":480,"caption":"https://ko.wikipedia.org/wiki/%ED%9E%99\_(%EC%9E%90%EB%A3%8C\_%EA%B5%AC%EC%A1%B0)","filename":"glq.png"}\_\#\#\]

 

 

 

## 참고자료

**위키백과**

<https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%83%9D>

<https://ko.wikipedia.org/wiki/%ED%81%90_(%EC%9E%90%EB%A3%8C_%EA%B5%AC%EC%A1%B0)> 

<https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%A6%AC_%EA%B5%AC%EC%A1%B0>

<https://ko.wikipedia.org/wiki/%ED%9E%99_(%EC%9E%90%EB%A3%8C_%EA%B5%AC%EC%A1%B0)> 

 

**개발 블로그**

<https://velog.io/@wjdqls9362/Algorithm-Binary-Heap-%EC%9D%B4%EC%A7%84-%ED%9E%99> 

[](https://velog.io/@wjdqls9362/Algorithm-Binary-Heap-%EC%9D%B4%EC%A7%84-%ED%9E%99)

<div class="og-image" style="background-image: url(&#39;https://scrap.kakaocdn.net/dn/bj5hJI/hyNmAxZJDa/35jhGtrAJotthj9i7IVRH0/img.png?width=950&amp;height=500&amp;face=0_0_950_500&#39;);">

 

</div>

<div class="og-text">

\[Algorithm\] Binary Heap (이진 힙)

이진 힙에 알고리즘에 대해서 학습한다.Binary Heap(이진 힙) 은 노드의 값이 특정한 순서를 가지고 있는 완전 이진
트리(Complete Binary Tree)다.완전 이진 트리는 마지막 레벨을 제외하고 모든 이진 트

velog.io

</div>

<https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html>

[](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

<div class="og-image" style="background-image: url();">

 

</div>

<div class="og-text">

\[자료구조\] 힙(heap)이란 - Heee's Development Blog

Step by step goes a long way.

gmlwjd9405.github.io

</div>

<https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html>

[](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)

<div class="og-image" style="background-image: url();">

 

</div>

<div class="og-text">

\[자료구조\] 트리(Tree)란 - Heee's Development Blog

Step by step goes a long way.

gmlwjd9405.github.io

</div>

<https://wayhome25.github.io/cs/2017/04/19/cs-23/>

[](https://wayhome25.github.io/cs/2017/04/19/cs-23/)

<div class="og-image" style="background-image: url();">

 

</div>

<div class="og-text">

강의노트 22. 자료구조 - tree(트리), heap(힙) · 초보몽키의 개발공부로그

패스트캠퍼스 컴퓨터공학 입문 수업을 듣고 중요한 내용을 정리했습니다. 개인공부 후 자료를 남기기 위한 목적임으로 내용 상에 오류가
있을 수 있습니다.

wayhome25.github.io

</div>

<https://ddunnimlabs.tistory.com/104>

[](https://ddunnimlabs.tistory.com/104)

<div class="og-image" style="background-image: url(&#39;https://scrap.kakaocdn.net/dn/c0oKz3/hyNlqjtHER/r14a775oojJXthqbsAEtoK/img.png?width=371&amp;height=664&amp;face=0_0_371_664,https://scrap.kakaocdn.net/dn/bD614Q/hyNmz6U2ew/6Jv7JIkEl1AYMSwt1PKYk0/img.png?width=371&amp;height=664&amp;face=0_0_371_664,https://scrap.kakaocdn.net/dn/dXn8AZ/hyNmI3RvAM/leVLo4mjutldQeL3Km39dK/img.png?width=1013&amp;height=437&amp;face=0_0_1013_437&#39;);">

 

</div>

<div class="og-text">

Stack , Queue, Heap 의 구조와 메모리 영역에 대한 이해

최근들어 프로그래밍에 알고리즘과 자료구조의 중요성을 느낀다. 확실히 한단계 더 높은 개발자가 되려면 기초가 중요하고 알고리즘과
자료구조의 중요성이 더욱 강해지는 것 같다.. 주변 개발

ddunnimlabs.tistory.com

</div>
