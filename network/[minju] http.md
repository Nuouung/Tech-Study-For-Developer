![](https://images.velog.io/images/tlsrlgkrry/post/30694b95-7fe9-486a-9a11-804359862e88/image.png)

### 1. HTTP란? 
---
HTTP : 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 프로토콜
- `프로토콜` : 컴퓨터나 원거리 통신 장비 사이에서 메시지를 주고 받는 양식과 규칙 체계

HTTP는 <span style='color: orange'>**TCP/IP 기반**</span>으로 되어있으며 
클라이언트가 요청을 생성하기 위한 연결을 연 다음 응답을 받을 때까지 대기하는 전통적인 <span style='color: orange'>**클라이언트-서버 모델**</span>을 따릅니다.
웹 브라우저와 웹 서버간의 통신 방법이므로 <span style='color: orange'>**애플리케이션 계층**</span>의 프로토콜입니다.
내부적으로 Transport 계층의 TCP를 이용하지만, HTTP 자체는 애플리케이션 계층의 프로토콜입니다.
- `클라이언트 서버 구조` : Request, Response 구조, 클라이언트는 서버에 요청을 보내고 응답은 대기하며 서버는 요청에 대한 결과를 만들어서 응답하는 구조
<br><br>
### 2. HTTP 특징
---
#### 1. 비연결성 (Connectionless)
<span style='color: orange'>__비연결성 (Connectionless)__</span> : 클라이언트와 서버가 한 번 연결을 맺은 후, 클 라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어 버리는 성질

- 장점 )
HTTP는 인터넷 상에서 불특정 다수의 통신환경을 기반으로 설계되었습니다. 
만약 연결을 계속 유지해야 한다면, 많은 리소스가 발생합니다.
연결을 유지하기 위한 리소스를 줄이면 **더 많은 연결이 가능**합니다.

- 단점 )
연결 경험이 있는 클라이언트라도 비연결성 특징 때문에 모든 요청에 대한 연결/해제 과정을 거처야하므로 **연결/해제에 대한 오버헤드가 발생(3 way handshake)**합니다.

#### 2. 무상태성 (Stateless)
<span style='color: orange'>**무상태성 (Stateless)**</span> : 비연결성(Connectionless)로 인해 서버는 클라이언트를 식별할 수 없는데 이를 무상태성이라고 합니다. 이전의 정보나 현재 통신의 상태가 남아 있지 않습니다.

- 장점 )
각각의 통신이 독립적으로 관리되어 서버 확장성이 높습니다(스케일 아웃)

- 단점 )
 클라이언트의 상태를 유지할 수 없어 요청마다 추가적인 정보가 필요합니다.
 
>비연결성과 무상태성이라는 특징때문에 모든 요청마다 인증을 해야합니다.
이러한 문제를 해결하기 위해 상태를 기억하도록 도와주는 여러가지 방법이 있는데 쿠키, 세션, 토큰 등이 있습니다.

### 3. HTTP 구성
---

### 4. HTTP Status Code

### 5. HTTP Method

### . TCP/IP, UDP



![](https://images.velog.io/images/tlsrlgkrry/post/8138df73-4ed9-4cc2-a4f2-884e91acb909/img.png)

### 참고 사이트
[[Network] HTTP 개념 정리](https://ngwoon.github.io/network/2020/08/07/HTTP-HTML/)
[[Web 기초] HTTP 통신 과정](https://mysterico.tistory.com/29)
[HTTP란 무엇인가?](https://velog.io/@surim014/HTTP%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
[[HTTP] HTTP 특성(비연결성, 무상태)과 구성요소 그리고 Restful API](https://victorydntmd.tistory.com/286)