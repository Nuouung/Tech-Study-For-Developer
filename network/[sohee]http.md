## HTTP
- Hyper Text Transfer Protocol의 두문자어로, 인터넷에서 데이터를 주고받을 수 있는 프로토콜(규칙)이다. 이렇게 규칙을 정해두었기 때문에, 모든 프로그램이 이 규칙에 맞춰 개발해서 서로 정보를 교환할 수 있게 됨
- TCP/ IP를 이용하는 응용 프로토콜
- 연결을 유지하지 않는 프로토콜이기 때문에 요청/응답 방식으로 동작
- 클라이언트가 서버에 요청을 보내면 서버는 그에 대한 응답을 보내는 클라이언트 서버 구조
- 클라이언트의 상태를 보존하지 않는 Stateless & HTTP 1.0 기준으로 연결을 유지하지 않는 Connectionless
    - 만약 Stateful하다면 항상 같은 서버가 유지 되어야 하고 서버에 장애가 생긴다면 상태정보가 다 날아가버리므로 처음부터 다시 서버에 요청해야 한다. 하지만 Stateless는 아무 서버나 호출해도 된고 만약 서버에 장애가 생긴다면 다른 서버에 요청하면 되며 스케일 아웃이 가능하다
    - Connectionless는 매번 TCP/IP 연결을 새로 맺어야 해서 3 way handshake 시간이 추가된다.
- 전체 인터넷 프로토콜에서 위치하는 곳은 응용계층이다
    - 응용 계층 (DNS, FTP, HTTP)
    - 전송 계층 (TCP,UDP,SCTP)
    - 네트워크 계층 (IP,ARP,RARP)
    - 링크 계층 (이더넷, WIFI, 토큰링)

## HTTP 메시지

- 요청 헤더 구성
    - Start line : 메서드 사이트주소 버전 ex)GET [https://www.zerocho.com](https://www.zerocho.com/) HTTP/1.1
    - Headers : 요청에 대한 정보
    - Body : 헤더에서 한 줄 띄고 시작되며 요청을 할 때 함께 보낼 데이터를 담는 부분
- 응답 헤더 구성
    - Start line : 버전 상태코드 상태메시지 ex) HTTP/1.1 200 OK
    - Headers : 응답에 대한 정보
    - Body : 클라이언트가 요청한 데이터

# HTTP Header

- General header : 요청과 응답에 모두 적용되지만, 데이터와는 관련이 없는 헤더
- Request header : 요청하는 클라이언트의 대한 자세한 정보를 포함하는 헤더
- Response header : 서버 자체에 대한 정보, 응답에 대한 부가적인 정보를 포함하는 헤더
- Entity header : 컨텐츠의 길이나 MIME 타입과 같이 엔티티 바디에 대한 자세한 정보를 포함하는 헤더

## 요청/응답 공통 헤더

- Date : HTTP 메시지가 만들어진 시각. 자동으로 만들어짐
- Connection : HTTP/1.1에서는 기본적으로 keep-alive로 되어있는데 HTTP/2에서는 아예 사라져버림.
- Cache-Control (중요)
- Content-Length : 요청과 응답 메시지의 본문 크기를 바이트 단위로 표시해줌 메시지 크기에 따라 자동으로 만들어짐
- Content-Type : 컨텐츠의 타입(MIME)과 문자열 인코딩(utf-8 등등)을 명시
- Content-Language : 사용자의 언어
- Content-Encoding : 컨텐츠 압축된 방식입니다. 응답 컨텐츠를 br, gzip, deflate 등의 알고리즘으로 압축해서 보내면, 브라우저가 알아서 해제해서 사용

## 요청 헤더

- Host : 포트 포함한 서버의 도메인 네임
- User-Agent : 현재 사용자가 어떤 클라이언트(운영체제와 브라우저 같은 것)를 이용해 요청을 보냈는지, 이를 통해 접속자 통계를 낼 수 있고,  IE로 접속한 사람들을 찾아낸 후, IE는 지원하지 않으니 크롬으로 접속해주세요와 같은 메시지를 표시함
- Accept : 요청을 보낼 때 서버에 이런 타입(MIME)의 데이터를 보내줬으면 좋겠다고 명시
    - Accept-Encoding : 문자 인코딩(UTF-8 등)을 명시하
    - Accept-Charset :원하는 언어
    - Accept-Language : 원하는 컨텐츠 압축 방식
- Authorization : 인증 토큰(JWT든, Bearer 토큰이든)을 서버로 보낼 때 사용
- Origin : POST같은 요청을 보낼 때, 요청이 어느 주소에서 시작되었는지를 나타냄. 요청을 보낸 주소와 받는 주소가 다르면 CORS 문제가 발생하기도 함

## 응답 헤더

- Access-Control-Allow-Origin : 요청을 보내는 프론트 주소와 받는 백엔드 주소가 다르면 CORS 에러
가 발생하는데요. 이 때 서버에서 응답 메시지 Access-Control-Allow-Origin 헤더에 프론트 주소를 적어주어야 에러가 나지 않습니다.
- Allow : 서버가 허용하는 메서드와 헤더를 응답. ex) 405 Method Not Allowed 에러를 응답하면서 헤더로 [Allow: GET]를 같이 보냄
- Content-Disposition : 응답 본문을 브라우저가 어떻게 표시해야 할지 알려주는 헤더
- Location : 300번대 응답이나 201 Created 응답일 때 어느 페이지로 이동할지를 알려주는 헤더
- Content-Security-Policy : 다른 외부 파일들을 불러오는 경우, 차단할 소스와 불러올 소스를 명시

## 캐시 헤더

- Cache-Control : 캐시를 어떻게 사용할 것인지,  max-age로 캐시 유효시간을 줄 수 있다
- Age : 캐시 응답 때 나타나는데, max-age 시간 내에서 얼마나 흘렀는지 초 단위로 알려줌
- Expires : 응답 컨텐츠가 언제 만료되는지를 나타내며, Cache-Control의 max-age가 있는 경우 이 헤더는 무시
- ETag : 컨텐츠가 바뀌었는지를 검사할 수 있는 태그

## 쿠키 헤더

- Set-Cookie : 서버에서 클라이언트(브라우저)한테 이런 이런 쿠키를 저장하라고 명령하는 응답 헤더
- Cookie : 라이언트가 서버한테 쿠키를 보내줄 때

## HTTP 동작

- 클라이언트가 어떠한 서비스를 요청(request)을 하면 서버에서는 해당 요청사항에 맞는 결과를 찾아서 사용자에게 응답(response)하는 형태로 동작한다.

# Statue Code 종류

- 1XX (조건부 응답) : 서버가 요청을 받아 처리 중을 나타냄. 현재는 거의 사용하지 않는다.
- 2XX (성공) : 클라이언트 요청을 성공적으로 처리했음
    - 200 OK: 클라이언트의 성공적으로 처리
- 3XX (리다이렉션 완료) : 클라이언트는 요청을 마치기 위해 추가 동작을 취해야 한다.
    - 302 Found: 요청된 리소스의 URI가 일시적으로 변경됐음
- 4XX (요청 오류) : 클라이언트가 잘못된 요청을 했을 경우 발생
    - 400 Bad Request: 요청이 잘못되었을 때를 나타냄.
    - 401 Unauthorized: 인증이 필요한 리소스에 인증없이 접근할 때 발생.
    - 403 Forbidden: 서버까지 클라이언트 요청이 도착했으나 접근 권한이 없음.
    - 404 Not Found: 서버가 요청된 리소스를 찾을 수 없음. 가장 흔한 오류.
    - 408 Request Timeout: 요청 중 시간이 초과되었을 때 사용.
- 5XX (서버 오류) : 서버가 클라이언트의 요청을 처리하지 못했을 때 발생
    - 500 Internal Server Error: 서버 문제로 인한 오류. 보통은 서버측 오류임.
    - 502 Bad Gateway: 게이트웨이가 연결된 서버에서 잘못된 응답을 받았을 때. 보통 서버 폭주시 발생.

# HTTP 메서드

- HTTP 요청의 동작을 설명

- GET
    - 데이터를 요청할 떄 사용하며 url에 데이터를 붙여서 서버로 데이터를 보내기 때문에 보낼 수 있는 정보량이 한계가 있고 정보가 노출된다.
- POST : 데이터를 생성
- PUT : 데이터를 전체수정
- PATCH : 데이터를 부분 수정
- DELETE :데이터를 삭제
- OPTIONS : 서버에서 지원하는 메소드 확인

# HTTP 버전별 차이

## HTTP/1.0

- 헤더, 상태코드, content-type 새로 생김
- 커넥션당 1개의 요청-응답이 이루어짐

## HTTP/1.1

- 대부분의 웹 환경은 1.1을 따르는 중
- persistent connection으로 지정한 timeout 동안 커넥션을 닫지 않는 방식
- 파이프 라이닝 도입 : 하나의 커넥션에서 응답을 기다리지 않고 순차적인 여러 요청을 연속적으로 보내 그 순서에 맞춰 응답을 받는 방식으로 지연 시간을 줄이는 방법
    - 문제점
        
        Head Of Line Blocking 
        
        첫번쨰 요청에 문제가 생기면 뒤에 요청들은 대기해야해서 병목 현상이 발생 
        
        Header 중복 
        
        연속된 요청은 헤더가 같을 경우가 많은데 이를 중복해서 보내야함 
        

## HTTP/2

- 병렬 요청 가능
- 기존보다 성능 향상에 초점을 맞춘 버전으로 멀티플렉싱, 헤더압축, 서버푸시를 지원
- HTTP 메시지 전송 방식의 변화 : 기존에는 text를 전송했지만, 메시지 전송 방식의 변화를 줘서 바이너리 프레이밍 계층을 사용해 파싱과 전송 속도를 높이고 오류 발생 가능성을 낮췄다
- request and response multiplexing 으로 Head Of Line Blocking 해결
- 리소스간 우선 순위 설정이 가능
- server push
- header compression : 헤더의 크기를 줄여 페이지 로드 시간 감소
    - static dynamic table이라는 개념을 도입해서 요청간 중복을 검출해 중복된 것은 인덱스만 뽑아서 보냄
- TCP Head Of Line Blocking 문제 있음 : 스트림이 병렬로 처리되고 있을 때 중간에 있는 데이터 손실 시 뒤에 데이터가 모두 대기하게 됨

# QUIC

- UDP기반의  전송 계층 프로토콜
    - UDP를 선택한 이유 : TCP는 신뢰성을 확보하기 위해 헤더에 여러 데이터들이 있어 지연을 줄이기 힘들지만 UDP는 데이터 전송에 집중한 설계로 원하는 기능 구현이 가능해서 TCP 지연을 줄이면서 TCP 만큼 신뢰성 확보 가능
- 전송 속도 향상
- 구글 제품 대부분의 프로토콜
- 첫 연결 요청 시 필요한 정보와 함께 전송한다. 연결 성공 시 connection uuid라는 고유한 식별자로 서버와 연결되는데 이을 캐싱해 다음 연결 때 handshake없이 통신 가능 하다
- TLS 기본 적용
- 독립 스트림을 써서 멀티 플레싱 지원

---

## HTTP/3

- QUIC을 바탕으로 한 HTTP

# HTTPS

- HyperText Transfer Protocol over Secure Socket Layer'의 약자로 간단히 말하면 통신 보안이 강화된 'HTTP’이다. 일반적으로 'SSL' 또는 'TSL' 프로토콜을 이용해 데이터를 암호화한다.

# HTTPS 동작 과정

1. 웹브라우저가 서버에 접속을 하면 서버는 CA기업이 서버의 정보를 CA 기업의 개인 키로 암호화한 인증서를 전달한다.
2. 웹브라우저는 이미 알고 있던 인증기관의 공개키로 인증서를 해독하여 검증한다. 이 해독을 통해 서버의 정보와 서버의 공개키를 알 수 있게 된다.
3. 클라이언트는 이렇게 얻은 서버의 공개키로 대칭키를 암호화해서 서버에 보낸다.
4. 서버는 개인키로 그를 해독해 대칭키를 얻게 되고, 이제 그 대칭키로 데이터를 암호화하여 주고받을 수 있게 된다.

대칭키 방식 : 암호화/복호화 시, 동일한 키를 사용
공개키(비대칭키) 방식 : 두 개의 키로 암호화/복호화를 진행. 암호화를 A키로 했다면 복호화는 B로, 암호화를 B로 했다면 복호화는 A로 해야 하는 식이다. 두 키 중 하나를 개인키(키 주인만 소유)로 지정하고, 다른 하나는 공개키(누구나 가질 수 있음)로 지정

# TCP

# TCP의 3-Way handshake & 4-Way hadnshake

- 3-Way-Handshaking
    - TCP 통신을 하기 위해 네트워크 연결을 설정하는 과정입니다. 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장한다.
    1. Client에서 Server에 연결 요청을 하기위해 SYN 데이터를 보내고 Client의 상태는 SYN을 보냈다는 의미인 SYN_SENT 상태가 됩니다
    2. Server에서는 SYN 데이터를 받고 클라이언트에게 요청을 수락한다는 ACK와 Client도 포트를 열어달라는 SYN 을 같이 보내고 Client가 다시 ACK으로 응답하기를 기다린다. Server는 SYN_RECEIVED 상태가 됩니다
    3. Client에서는 SYN+ACK를 받고 ESTABLISHED(포트 연결 상태)로 상태를 변경하고 서버에 ACK를 전송한다.
    4. ACK를 받은 서버는 상태가 ESTABLSHED로 변경된다.
    이를통해 연결이 됩니다.
- 4-Way-Handshaking
    - TCP 연결을 해제할 때 사용합니다.
    1. 통신을 종료하고자 클라이언트가 서버에게 FIN 패킷을 보내고 자신은 FIN_WAIT_1 상태로 대기한다.
    2. FIN 패킷을 받은 서버는 해당 포트를 CLOSE_WAIT 상태로 바꾸고 ACK를 클라이언트에게 보내고
    ACK를 받은 클라이언트는 상태를 FIN_WAIT_2 상태로 변경한다. 그와 동시에 서버에서는 해당 포트에 연결되어 있는 Application에게 Close()를 요청한다.
    3. Close() 요청을 받은 Application은 종료 프로세스를 진행시켜 최종적으로 Close()가 되고 서버는 FIN 패킷을 클라이언트에게 전송하고 상태를 LAST_ACK 상태로 바꾼다.
    4. 클라이언트는 FIN_WAIT_2 상태에서 서버가 연결을 종료했다는 신호를 기다리다가 FIN을 받으면 확인 했다는 의미로 ACK를 서버에게 전송한다. 그리고 클라이언트는 TIME_WAIT 상태로 바꾼다. TIME_WAIT 상태에서 일정 시간이 지나면 CLOSED 되게 된다.
    5, 최종 ACK를 받은 서버는 자신의 포트도 CLOSED로 닫게 된다.

# UDP

- 비연결형 프로토콜로 보내는쪽에서 일방적으로 데이터를 전달합니다. 정보를 주고 받을때 TCP 같은 신호절차를 거치지 않아 신뢰성이 없으며 TCP 상대적으로 시간이 빠릅니다. 스트리밍 서비스나 게임에서 사용한다.
- 패킷 오버헤드가 적어 네트워크 부하 감소
- 사용 사례
    - 스트리밍 서비스 : 동영상 디코딩은 구역별로 나눠서 인코딩하기에 데이터 손실이 몇 개 발생해도  일부 구역이 제대로 안나오는 정도이다.
    - 게임 서버 : 스킬 연타할 때 중간에 키보드 입력 한두 개가 빠졌다고 그 뒤의 입력이 전부 스톱 되면 유저는 답답함을 느낄 것이다. 이런 경우 자체적으로 복구하거나 아예 무시해버린다

# [www.google.com](http://www.google.com/) 을 웹 브라우저에 입력하면 무슨일이 일어날까?

---

1. 브라우저는 URL을 해석해 문법이 맞는지 확인하고, 캐싱된 DNS 기록들을 통해 해당 도메인 주소와 대응하는 IP주소가 있는지 확인한다. 기록에 없을 경우 DNS에게 도메인 주소의 IP를 요청
2. DNS가 IP주소를 찾아 브라우저에게 응답하면 해당 주소에 TCP 연결 작업 진행한다
3. TCP로 연결되면 웹브라우저가 GET 요청을 통해 서버에게 html문서를 요청
4. 서버가 WAS/DB등을 통해 웹페이지 작업을 처리하고 HTTP response를 보낸다
5. 브라우저는 화면에 HTML content를 보여준다

# CORS

- 웹 브라우저에서 외부 도메인 서버와 통신하기 위한 방식을 표준화한 HTTP 헤더 기반 메커니즘
- 서버쪽에서 클라이언트를 대상으로 리소스의 허용 여부를 결정하는 방법이다.
- 예전에는 자원을 저장하는 서버와 웹 페이지가 하나의 서버에서 만들어졌다.때문에 해당 서버의 자원은 해당 도메인에서만 요청하는 것이 당연했다.당연히 보안을 위해서 브라우저는 다른 도메인에서 서버의 자원을 요청할 경우를 막아 놓았다.그런데 시간이 지나 웹 기술이 발전하였고 페이지와 자원을 분리하거나 다른 서버의 자원을 요청을 보내는 경우가 많이 생겼다.어떻게 했냐하면 개발자들은 편법을 이용해서 다른 서버의 자원을 가져다썼다. (편법의 설명은 생략한다.)이런 일이 많아졌다고 브라우저에서 편법을 막아버리면 여러 사이트에서 문제가 발생할 수 있기 때문에 웹 브라우저에서 외부 도메인 서버와 통신하기 위한 방식을 표준화한 것을 만들었다.브라우저는 편법을 쓰기보다는 공식적으로 외부 도메인 자원을 가져다 쓰라고 만든것이 CORS이다.이러한 교차 출처 자원 공유 방식은 요청을 받은 웹서버가 허용할 경우에는 다른 도메인에서도 자원을 주고 받을 수 있게 해준다.

# URI vs URL

- URI
    - 네트워크 상에서 자원을 식별하기 위한 문자열의 구성
    - URL을 포함한다
- URL
    - 네트워크 상의 자원의 위치를 나타내는 주소

ex) [https://surprisecomputer.tistory.com/user/123](https://surprisecomputer.tistory.com/user/123) 의 경우 
URL은 [https://surprisecomputer.tistory.com/user](https://surprisecomputer.tistory.com/user) 까지고 원하는 정보에 도달하기 위한 식별자 123을 포함하면 URI

# 프로토콜

## OSI 참조 모델

- 데이터 통신을 단계로 나누어 각 단계의 순서를 명확히하고 모델에 따라 프로토콜을 정의해서 데이터 통신을 구축하려고하였다.즉, OSI 참조 모델은 데이터 통신의 단계와 순서의 설계도이다.
- OSI 참조 모델은 데이터 통신을 7개의 단계로 나눈다.
- 이 단계를 계층(Layer: 레이어)라고 부르며 각 계층마다 각각의 역할과 규칙이 있다.
- 네트워크에 의한 데이터 통신은 단계마다 복수의 프로토콜로 실현된다.
- 데이터 통신을 할 때 7계층에서 1계층으로 각각의 순서를 단계적으로 수행함으로써 데이터 통신이 가능해진다.
- OSI 참조 모델의 장점은 계층이 각각 독립해 있어서 어떤 계층의 프로토콜 변경은 다른 계층에 영향을 끼치지 않는다는 것이다.
- 기본적으로 하위 계층은 상위 계층을 위해서 일하고 상위 계층은 하위 계층에 관여하지 않는다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b3cc13b1-54b5-4e50-a51a-553c3c6a04e0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220223%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220223T143739Z&X-Amz-Expires=86400&X-Amz-Signature=4b2d72a9bfc3c39a6a6e13482d759a9eb44d69a5d6593598d069ca1f44765cc0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

### 응용 계층 (Application)

- 네트워크를 통해 송수신된 이진 데이터를 인코딩, 디코딩 하는 방법(메타 정보)을 넘겨주는 것
- 사용자가 OSI 환경에 접근할 수 있도록 프로토콜을 이용해서 서비스를 사용하는 것
- HTTP, DTP, SMTP

### 표현 계층 (Presentation)

- 응용 계층에서 받은 데이터를 세션 계층에 맞게 변환하거나, 세션 계층에서 받은 데이터를 응용 계층에 맞게 변환한다.
- ex) 코드 변화, 데이터 암호화, 데이터 압축, 구문 검색, 정보 형식 변환

### 세션 계층 (Session)

- 송수신측 간의 관련성을 유지시키고 대화 제어를 담당한다.
- ex) 동기 제어, 데이터 교환 관리

### 전송 계층 (Transport)

- port 번호를 사용해 도착지 컴퓨터의 최종 도착지인 프로세스에 까지 데이터가 도달하게 하는 모듈
- TCP/UDP 인지에 대한 정보와 출발지/도착지 포트번호 = 세그먼트
- 운영체제 커널에 sw적으로 구현되어 있다
- 전송 할 수 있게 연결을 설정 및 해제
- 데이터가 실제 전송되는 구간
- ex) 게이트웨어(출입문),  TCP, UDP

### 네트워크 계층 (=망계층) (Network)

- 수많은 네트워크들의 연결로 이루어지는 inter-network 속에서 어딘가에 있는 목적지 컴퓨터로 데이터를 전송하기 위해 ip 주소를 이용해 길을 찾고 (routing) 자신 다음의 라우터에게 데이터를 넘겨주는 것
- IP 주소를 이용해 서로 다른 네트워크에 속한 컴퓨터끼리 데이터를 주고 받게 해주는 것
- 전송계층에서 받은 데이터 + 출발지/도착지 IP 정보 = 패킷
- 운영체제 커널에 sw적으로 구현되어 있다
- 네트워크 연결을 관리한다. (경로 설정, 연결, 해제, 패킷 전송)
- 데이터 교환의 중계한다.
- ex) 라우터(서로 다른 네트워크에 속한 컴퓨터끼리 통신이 가능하게 해주는 장비, 네비게이션, 최적의 경로 찾아준다.)

### 데이터 링크 계층 (Data Link)

- 같은 네트워크에 있는 컴퓨터들이 데이터를 주고 받기 위해서 필요한 계층
- 하드웨어적으로 구현되어 있음
- 두 개의 인접한 개방 시스템들 끼리 신뢰성있고 효율적인 정보 전송 가능하게 한다.
- 흐름 제어, 프레임 동기화, 오류 제어, 순서 제어 기능
- 링크(찾아가는 길) 확립, 유지, 단절을 제공한다.
- ex) 랜카드, 브리지, 스위치

### 물리 계층 (Physical)

- 물리적으로 연결된 두 대의 컴퓨터가 데이터를 송수신할 수 있게 해주는 모듈
- 0과 1의 나열을 아날로그 신호로 바꿔 전선으로 흘려 보내고 아날로그 신호가 들어오면 0과 1의 나열로 해석해 물리적으로 연결될 두 대의 커퓨터가 0과 1의 나열을 주고 받을 수 있게 해주는 모듈
- framing :
- 1계층은  하드웨어적으로 구현되어 있음
- 전송에 필요한 두 장치간 실제 접속과 절단 등 기계적, 전기적, 기능적, 절차적 특성을 정의한다.
- 전기 신호를 전송한다. (만든다.)
- 제어 신호를 전송한다.
- 클럭 신호를 전송한다.
- ex)  리피터(증폭기), 허브
