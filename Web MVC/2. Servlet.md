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
HTTP요청 메시지를 개발자가 직접 파싱하는 대신, 서플릿이 개발자 대신 HTTP 요청 메시지를 파싱한다. 그리고 그 결과를 `HTTPServletRequest` 객체에 담아서 제공해준다

#### HTTP 요청 메시지
<img width="814" alt="스크린샷 2022-02-16 오후 1 38 39" src="https://user-images.githubusercontent.com/80378041/154197272-0695e6cf-c19d-4da1-8431-598c911b9589.png">

- HTTP 메소드, URL, 쿼리 스트링, 스키마, 프로토콜, 헤더 조회, form 파라미터 형식 조회, message body 데이터 직접 조회 뿐만 아니라 
  HTTPServletRequest는 여러가지 부가 기능도 함꼐 제공한다(임시 저장소 기능, 세션 관리 기능)
  
#### 임시 저장소 기능
- 해당 HTTP 요청이 시작부터 끝날 때까지 유지되는 임시 저장소 기능
  - 저장 : request.setAttribute(name, value)
  - 조회 : request.getAttribute(name)

#### 세션 관리 기능
- request.getSession(create: true)

> __HttpServletRequest,HttpServletResponse는 결국 HTTP 요청, 응답 메시지를 편리하게 사용하도록 도와주는 객체라는 점이다.__
> 
> __따라서 이 기능을 이해하려면 HTTP 자체의 요청, 응답 메시지를 알아야 한다__

## HTTP 요청 데이터

### GET - 쿼리 파라미터
- /url?username=hello&age=20
- 메시지 바디 없이 URL의 쿼리 파라미터에 데이터를 포함해서 전달
- 검색, 필터, 페이징 등에서 많이 사용하는 방식
- 쿼리 파라미터는 URL에 ?를 시작으로 보냄. 추가 파라미터는 &로 구분함

#### 쿼리 파라미터 조회 메서드
```java
String username = request.getParameter("username"); //단일 파라미터 조회
Enumeration<String> parameterNames = request.getParameterNames(); //파라미터 이름들 모두 조회
Map<String, String[]> parameterMap = request.getParameterMap(); //파라미터를 Map으로 조회
String[] usernames = request.getParameterValues("username"); //복수 파라미터 조회
```

#### 복수 파라미터에서 단일 파라미터 조회
`username=hello&username=kim`과 같이 파라미터 이름은 하나인데 값을 중복으로 쓸 수도 있다.
`request.getParam()`는 하나의 파라미터 이름에 하나의 값이 매칭 될 때 사용해야 한다. 위처럼 중복인 경우에는 `request.getParamValues()`를 사용해야 한다
중복인 경우에 `request.getParam()`를 사용하면 첫번 째 값인 hello를 반환하게 된다.

### POST - HTML FORM
- content-type: application/x-www-form-urlencoded
- 메시지 바디에 쿼리 파라미터 형식으로 전달 `username=hello&age=20`
- 회원가입, 상품주문, HTML Form 사용
- `application/x-www-form-rulencoded` 방식은 위의 GET - 쿼리 파라미터 형식과 동일하다. 따라서 쿼리 파라미터 조회 메서드를 그대로 재사용 가능
- HTTP 메시지 바디가 필요하기 때문에 바디에 포함된 데이터가 어떤 형식인지 content-type을 꼭 지정해주어야 함

#### Postman을 이용한 테스트
간단한 테스트에 HTML Form을 만들기는 귀찮을 때, Postman 프로그램을 사용할 수 있다

### API 메시지 바디
- HTTP message body에 직접 데이터를 담아서 요청
  - HTTP API에서 주로 사용, JSON, XML, TEXT
  - 데이터 형식은 주로 JSON 사용
  - POST, PUT, PATCH
- HTTP 메시지 바디의 데이터를 InputStream을 사용해서 직접 읽을 수도 있다
  - InputStream은 byte코드를 반환한다. byte 코드를 우리가 읽을 수 있는 문자로 보려면 문자표(Charset)을 지정해주어야 한다


## HTTP ServletResponse

#### 역할
HTTP 응답코드를 지정하고, 헤더, 바디의 내용을 생성할 수 있고, Content-type, 쿠키, Redirect 등을 편리하게 다룰 수 있는 기능을 제공한다

### 기본 메서드
```java
        response.setStatus(HttpServletResponse.SC_OK); //상태를 설정해준다(200,300,400...)

        response.setHeader("Content-Type", "text/plain; charset=utf-8"); //헤더에 들어갈 내용들을 적어줄 수 있다.
        response.setHeader("Cache-Control", "no-cache,no-store,must-revalidate");
        response.setHeader("Pragma","no-cache");
        response.setHeader("my-header","hello");     
```

### Content 메서드
```java
   response.setContentType("text/plain"); // 응답 메시지의 타입을 정해준다
   response.setCharacterEncoding("utf-8"); // 응답 메시지를 무엇으로 인코딩 해줄 것인지 정해준다
   response.setContentLength(2); // 생략시 자동 생성된다

```

### Cookie 메서드
```java
      Cookie cookie = new Cookie("myCookie", "good"); // 쿠키 객체를 생성해준다
      cookie.setMaxAge(600); //600초로 저장 시간을 정해준다

      response.addCookie(cookie); // 쿠키를 응답에 넣어주는 메서드이다
```

### Redirect 메서드
```java
      response.sendRedirect("/basic/hello-form.html"); // redirect를 응답에 넣어주었다
```

### HTTP 응답 데이터 - 단순 텍스트, HTML

#### 단순 텍스트 응답
- `writer.println("message");`

#### HTML 응답
```java
PrintWriter writer = response.getWriter();
        writer.println("<html>");
        writer.println("<body>");
        writer.println("<div>안녕?</div>");
        writer.println("</body>");
        writer.println("</html>");
```
위의 형태로 html도 응답으로 보낼 수 있다. 이 때, Content-type은 `text/html`로 지정해주어야 한다.

#### HTTP API - JSON 응답
HTTP 응답으로 JSON을 보낼 때는 Content-Type으로 `application/json`을 지정해야 한다.
