![썸네일](https://images.velog.io/images/tlsrlgkrry/post/886ac100-51ba-4c43-8803-d9c409e584fd/image.png)

## 1. HTTP란? 
---
HTTP : 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 프로토콜
- `프로토콜` : 컴퓨터나 원거리 통신 장비 사이에서 메시지를 주고 받는 양식과 규칙 체계

HTTP는 <span style='color: orange'>**TCP/IP 기반**</span>으로 되어있으며 
클라이언트가 요청을 생성하기 위한 연결을 연 다음 응답을 받을 때까지 대기하는 전통적인 <span style='color: orange'>**클라이언트-서버 모델**</span>을 따릅니다.
웹 브라우저와 웹 서버간의 통신 방법이므로 <span style='color: orange'>**애플리케이션 계층**</span>의 프로토콜입니다.
내부적으로 Transport 계층의 TCP를 이용하지만, HTTP 자체는 애플리케이션 계층의 프로토콜입니다.
- `클라이언트 서버 구조` : Request, Response 구조, 클라이언트는 서버에 요청을 보내고 응답은 대기하며 서버는 요청에 대한 결과를 만들어서 응답하는 구조
<br><br>
---
## 2. HTTP 특징

### 1. 비연결성 (Connectionless)
<span style='color: orange'>__비연결성 (Connectionless)__</span> : 클라이언트와 서버가 한 번 연결을 맺은 후, 클 라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어 버리는 성질

- 장점 )
HTTP는 인터넷 상에서 불특정 다수의 통신환경을 기반으로 설계되었습니다. 
만약 연결을 계속 유지해야 한다면, 많은 리소스가 발생합니다.
연결을 유지하기 위한 리소스를 줄이면 **더 많은 연결이 가능**합니다.

- 단점 )
연결 경험이 있는 클라이언트라도 비연결성 특징 때문에 모든 요청에 대한 연결/해제 과정을 거처야하므로 **연결/해제에 대한 오버헤드가 발생(3 way handshake)**합니다.
<br>

### 2. 무상태성 (Stateless)
<span style='color: orange'>**무상태성 (Stateless)**</span> : 비연결성(Connectionless)로 인해 서버는 클라이언트를 식별할 수 없는데 이를 무상태성이라고 합니다. 이전의 정보나 현재 통신의 상태가 남아 있지 않습니다.

- 장점 )
각각의 통신이 독립적으로 관리되어 서버 확장성이 높습니다(스케일 아웃)

- 단점 )
 클라이언트의 상태를 유지할 수 없어 요청마다 추가적인 정보가 필요합니다.
 
>비연결성과 무상태성이라는 특징때문에 모든 요청마다 인증을 해야합니다.
이러한 문제를 해결하기 위해 상태를 기억하도록 도와주는 여러가지 방법이 있는데 쿠키, 세션, 토큰 등이 있습니다.

---

## 3. Request와 Response

![Request와 Response이미지](https://images.velog.io/images/tlsrlgkrry/post/568568c9-632d-4faa-8dbe-dccfcaca7c2a/96372822-b8a38e00-11a3-11eb-85f2-089a13dc9f36.png)

### 1. Request
<span style='color: orange'>Request(요청)</span> : client가 server에게 HTTP를 보내는 것, HTTP 패킷에 요청에 대한 정보를 담아야 한다.

#### HTTP Method
 : 주어진 리소스에 수행하길 원하는 행동을 설명

1. `GET` : __자료를 요청__할 때 사용 
	➡ 서버에 전달할 데이터는 query를 통해 전달
2. `POST` : 자료의 __생성을 요청__할 때 사용 
	➡ 서버에 전달할 데이터는 Body를 통해 전달
3. `PUT` : 자료의 __전체수정__을 요청할 때 사용 
    	  (리소스가 있으면 대체하고 없으면 생성)
4. `PATCH` : 자료의 __부분수정__을 요청할 때 사용
5. `DELETE` : 자료의 __삭제를 요청__할 때 사용
6. `OPTION` : 서버에서 지원되는 __메소드의 종류__를 확인할 경우 사용
<br>
### 2. Response

<span style='color: orange'>Response(응답)</span> : client가 server에게 HTTP를 보내는 것, HTTP 패킷에 요청에 대한 정보를 담아야 합니다.

#### HTTP 상태코드
 : 요청에 대한 응답이 성공적으로 완료되었는가를 알려주는 코드, 숫자 세자리로 이류어져 있으며 크게 다섯 부류로 나눌 수 있습니다.
 
 
1. `1XX (조건부 응답)` : 요청을 받았으며 작업을 계속한다.
2. `2XX (성공)` : 클라이언트가 요청한 동작을 수신하여 이해했고 승낙했으며 성공적으로 처리했음을 가리킨다.
3. `3XX (리다이렉션 완료)` : 클라이언트는 요청을 마치기 위해 추가 동작을 취해야 한다.
4. `4XX (요청 오류)` : 클라이언트에 오류가 있음을 나타낸다.
5. `5XX (서버 오류)` : 서버가 유효한 요청을 명백하게 수행하지 못했음을 나타낸다.

---

## 4. HTTP 구성

---

### 참고 사이트
[[Network] HTTP 개념 정리](https://ngwoon.github.io/network/2020/08/07/HTTP-HTML/)
[[Web 기초] HTTP 통신 과정](https://mysterico.tistory.com/29)
[HTTP란 무엇인가?](https://velog.io/@surim014/HTTP%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
[[HTTP] HTTP 특성(비연결성, 무상태)과 구성요소 그리고 Restful API](https://victorydntmd.tistory.com/286)