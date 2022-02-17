# HTTP(Hyper Text Transfer Protocol)

## HTTP 메시지에 모든 것을 전송
- HTML, TEXT
- Image,음성, 영상, 파일
- JSOM, XML (API)
- 거의 모든 형태의 데이터 전송 가능
- 서버 간에 데이터를 주고 받을 때도 대부분 HTTP 사용

## HTTP 역사
- HTTP/0.9 : GET 메소드만 지원, HTTP 헤더 X
- HTTP/1.0 : 메소드, 헤더 추가
- __HTTP/1.1 : 가장 많이 사용, 우리에게 가장 중요한 버전__
  - RFC2068 -> RFC2616 -> RFC7230~7235
- HTTP/2 : 성능 개선
- HTTP/3 : TCP 대신에 UDP 사용, 성능 개선

## 기반 프로토콜
- TCP : HTTP/1.1, HTTP/2
- UDP : HTTP/3
- 현재 HTTP/1.1을 주로 사용(HTTP/2,3 도 점점 증가)

## HTTP 특징
- 클라이언트 서버 구조
- 무상태 프로토콜(스테이스리스), 비연결성
- HTTP 메시지
- 단순함, 확장 가능

## 클라이언트 - 서버 구조
- Request, Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답
- 클라이언트가 단순한 작업만 할 수 있게 해줌
- 서버의 변경을 클라이언트에 관계없이 독립적으로 가능하게 함
<img width="908" alt="스크린샷 2022-02-17 오후 4 08 33" src="https://user-images.githubusercontent.com/80378041/154424156-ede181cf-b24c-4294-b261-536b56ac216a.png">

## 무상태 프로토콜(Stateless)
- 서버가 클라이언트의 상태를 보존 X
- 장점 : 서버 확장성이 높음(스케일 아웃)
- 단점 : 클라이언트가 추가 데이터 전송

### Stateful, Stateless 차이
- 상태 유지 : 중간에 서버가 바뀔 수 없음(다른 서버로 바뀔 때 상태 정보를 미리 넘겨줘야 한다)
  - 중간에 서버에 장애가 나면 문제가 발생
<img width="1085" alt="스크린샷 2022-02-17 오후 4 09 22" src="https://user-images.githubusercontent.com/80378041/154424173-4ae4b09f-5fd5-4690-88d3-bb96c4ac88dc.png">

- 무상태 : 중간에 다른 서버로 바뀌어도 됨
  - 갑자기 클라이언트 요청이 증가해도 서버를 늘릴 수 있음
<img width="1085" alt="스크린샷 2022-02-17 오후 4 09 33" src="https://user-images.githubusercontent.com/80378041/154424182-cefe4bb5-3da3-4e11-ada7-5799eb47cd89.png">

- 무상태는 응답 서버를 쉽게 바꿀 수 있음 -> __무한한 서버 증설 가능__(스케일 아웃 - 수평확장에 유리)

### Stateless의 한계
- 모든 것을 무상태로 설계할 수 있는 경우도 있고 없는 경우도 있다
- 무상태 ex) 로그인이 필요없는 단순한 서비스 소개 ㅘ면
- 상태 유지 ex) 로그인
- 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
- 일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 상태 유지
- 상태 유지는 최소한만 사용

## 비연결성
### 연결을 유지하는 모델
서버가 클라이언트와 연결을 유지하는 자원을 계속 소모하게 된다
<img width="1063" alt="스크린샷 2022-02-17 오후 4 09 51" src="https://user-images.githubusercontent.com/80378041/154424205-192cf538-cad2-4209-bfe8-aa5b1e81adc6.png">

### 연결을 유지하지 않는 모델
서버가 요청/응답이 끝나면 연결을 끊어버려서 서버가 최소한의 자원을 사용하게 된다
<img width="987" alt="스크린샷 2022-02-17 오후 4 10 15" src="https://user-images.githubusercontent.com/80378041/154424212-a2b63bb8-33c3-4475-a247-9da5a4263014.png">

### 비연결성
- HTTP는ㄴ 기본이 연결을 유지하지 않는 모델
- 일반적으로 초 단위 이하늬 빠른 속도로 응답
- 1시간동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
 - ex) 실제로 수천명이 동시에 검색버튼을 누르지 않는다
- 서버 자원을 매우 효율적으로 사용할 수 있음

### 비연결성 한계
- TCP/IP 연결을 새로 맺어야 함 - 3way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등 수많은 자원이 함께 다운로드
- 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
- HTTP/2, HTTP/3에서 더 많은 최적화
- HTTP 초기
<img width="605" alt="스크린샷 2022-02-17 오후 4 10 28" src="https://user-images.githubusercontent.com/80378041/154424250-78966609-ce5c-498f-afe1-184e3e73acc2.png">


- HTTP 지속 연결
<img width="597" alt="스크린샷 2022-02-17 오후 4 10 34" src="https://user-images.githubusercontent.com/80378041/154424260-1365b927-004a-4264-91e7-9682781e80e9.png">

## HTTP 메시지
### HTTP 요청 메시지
<img width="525" alt="스크린샷 2022-02-17 오후 4 11 26" src="https://user-images.githubusercontent.com/80378041/154424274-8fddda16-ff22-4253-9580-dcdc5aa4dc9f.png">

### HTTP 응답 메시지
<img width="529" alt="스크린샷 2022-02-17 오후 4 11 32" src="https://user-images.githubusercontent.com/80378041/154424288-04f723da-3503-47e9-bcf6-476674072f21.png">

### HTTP 메시지 구조
<img width="516" alt="스크린샷 2022-02-17 오후 4 11 36" src="https://user-images.githubusercontent.com/80378041/154424294-bf8f4f77-ed63-4b7a-8261-da936dee35f2.png">

#### 시작 라인
- 요청 메시지
  - start-line = __request-line__ / status-line
  - request-line = method SP (공백) request-target SP HTTP-version CRLF(엔터)
<img width="509" alt="스크린샷 2022-02-17 오후 4 11 46" src="https://user-images.githubusercontent.com/80378041/154424305-02b6365d-3951-4e38-abb4-bba0c526e17e.png">

- HTTP 메서드(GET: 조회) / 요청 대상(/search?q=hello&hl=ko) / HTTP version

- HTTP 메서드
  - 종류 : GET, POST, PUT, DELETE...
  - 서버가 수행해야 할 동작 지정(GET : 리소스 조회 / POST : 요청 내역 처리)
- 요청 대상
  - absolute-psth[?query] (절대경로?[쿼리])
  - 절대경로 = "/"로 시작하는 경로
- HTTP 버전

- 응답 메시지
  - start-line = request-line / __status-line__
  - status-line = HTTP-version SP status-code SP reason-phrase CRLF
<img width="421" alt="스크린샷 2022-02-17 오후 4 11 56" src="https://user-images.githubusercontent.com/80378041/154424324-91f7354e-ac77-4ee2-a326-be67a02c9451.png">

- HTTP 버전 / HTTP 상태 코드 : 요청성공, 실패를 나타냄(200 : 성공, 400 : 클라이언트 요청 오류, 500 : 서버 내부 오류) / 이유 문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명 글

#### HTTP 헤더
header-field = field-name ":" OWS field-value OWS (OWS : 띄어쓰기 허용)

field-name은 대소문자 구분 없음
<img width="506" alt="스크린샷 2022-02-17 오후 4 12 07" src="https://user-images.githubusercontent.com/80378041/154424341-f460f9b5-210d-44e8-9e57-8cfa24e3bf06.png">

- 용도
  - HTTP 전송에 필요한 모든 부가정보
  - 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라리언트 정보, 서버 애플리케이션 정보 등등...
  - 표준 헤더가 너무 많음
  - 필요 시 임의의 헤더 추가 가능

#### HTTP 메시지 바디
<img width="510" alt="스크린샷 2022-02-17 오후 4 12 16" src="https://user-images.githubusercontent.com/80378041/154424354-eea38d68-ba48-4ff8-a173-ab01ccf1bc14.png">

- 용도
  - 실제 전송할 데이터
  - HTML 문서, 이미지, 영상 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

### 단순함 확장 가능
- HTTP는 단순하다
- HTTP 메시지도 매우 단순
- 크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술!
