# 서블릿(Servlet)

### 서블릿 컨테이너 동작 방식
- 내장 톰캣 서버 생성
<img width="605" alt="스크린샷 2022-02-16 오후 12 37 13" src="https://user-images.githubusercontent.com/80378041/154191540-562e56cf-e2be-45c8-93ac-e65e847a56a0.png">

- HTTP 요청, 응답 메시지
<img width="607" alt="스크린샷 2022-02-16 오후 12 38 02" src="https://user-images.githubusercontent.com/80378041/154191641-ea82024d-9323-44bf-b333-6390c25b5ccd.png">

- 웹 애플리케이션 서버의 요청 응답 구조
<img width="608" alt="스크린샷 2022-02-16 오후 12 38 47" src="https://user-images.githubusercontent.com/80378041/154191726-16a7aea6-a13b-41f8-90d5-9428c2e61533.png">

- HTTP 응답에서 Content-Length는 웹 애플리케이션 서버가 자동으로 생성해준다.

## HTTP ServletRequest

#### 역할
HTTP요청 메시지를 개발자가 직접 파싱하는 대신, 서플릿이 개발자 대신 HTTP 요청 메시지를 파싱한다. 그리고 그 결과를 'HTTPServletRequest' 객체에 담아서 제공해준다

#### HTTP 요청 메시지
<img width="814" alt="스크린샷 2022-02-16 오후 1 38 39" src="https://user-images.githubusercontent.com/80378041/154197272-0695e6cf-c19d-4da1-8431-598c911b9589.png">

- HTTP 메소드, URL, 쿼리 스트링, 스키마, 프로토콜, 헤더 조회, form 파라미터 형식 조회, message body 데이터 직접 조회 뿐만 아니라 
  HTTPServletRequest는 여러가지 부가 기능도 함꼐 제공한다(임시 저장소 기능, 세션 관리 기능)


