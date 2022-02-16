# URI(Uniform Resource Identifier)

- URI는 로케이터, 이름 또는 둘 다 추가로 분류될 수 있다
<img width="661" alt="스크린샷 2022-02-16 오후 4 20 04" src="https://user-images.githubusercontent.com/80378041/154216963-c3f28691-b8e5-4cca-8616-325638d92aa0.png">

### URL과 URN의 구조
<img width="1091" alt="스크린샷 2022-02-16 오후 4 20 15" src="https://user-images.githubusercontent.com/80378041/154216996-49a3093f-e753-46ba-a1eb-623a16ba788b.png">

### URI의 단어 뜻

- Uniform : 리소스를 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 X)
- Identifier : 다른 항목과 구분하는데 필요한 정보

- URL - locator : 리소스가 있는 위치를 지정
- URN - name : 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다
- 하지만, URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화되지 않음


### URL 전체 문법
- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello&hl=ko

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트번호(443)
- 패스(/search)
- 쿼리 파라미터(q=hello&hl=ko)

#### scheme

- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
- http는 80포트, https는 주로 443 포트를 사용, 포트는 생략 가능
- https는 http에 보안이 추가됨

#### userinfo
- URL에 사용자 정보를 포함해서 인증
- 거의 사용하지 않음

#### PORT
- 접속 포트
- 일반적으로 생략, 생략 시 http는 80, https는 443

#### PATH
- 리소스 경로(path), 보통 계층적 구조
- ex) /home/file1.jpg, /members, /members/100, /items/iphone12

#### query
- key = value의 형태
- ?로 시작, &로 추가 가능(?keyA=valueA&keyB=valueB)
- query parameter, query string 등으로 불림, 웹 서버에 제공하는 파라미터. 문자 형태

#### fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보는 아님


-----------------------
# Web 브라우저 요청 흐름

### HTTP 요청 메시지
<img width="703" alt="스크린샷 2022-02-16 오후 4 29 51" src="https://user-images.githubusercontent.com/80378041/154217036-f80d46f3-b263-4140-a3db-00c7aa884acc.png">

### HTTP 메시지 전송 과정
<img width="987" alt="스크린샷 2022-02-16 오후 4 30 08" src="https://user-images.githubusercontent.com/80378041/154217049-307a36ad-a358-4d88-b84d-786e219ad58e.png">

### HTTP 응답 메시지
<img width="692" alt="스크린샷 2022-02-16 오후 4 30 29" src="https://user-images.githubusercontent.com/80378041/154217062-6ac7d077-8a29-4128-b016-67d5db1f2119.png">

### HTTP 응답 메시지를 받은 클라이언트
<img width="1089" alt="스크린샷 2022-02-16 오후 4 30 42" src="https://user-images.githubusercontent.com/80378041/154217080-0fb8a068-40c1-4fdc-8a7b-fba18be29887.png">
