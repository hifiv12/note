## chapter 1 JSP 기본

1. 동적 웹 페이지로의 여정과 jsp
  - 정적 웹페이지와 동적 웹페이지
    * 정적 웹페이지
      + 웹 브라우저 <-> 웹 서버 <-> HTML, 이미지등
    * 동적 웹페이지
      + 웹 브라우저 <-> 웹 서버 <-> 전처리 <-> 저장소 및 DB 

  - 발전 과정
    * 애플릿 
      + 자바 앱을 자바 가상 머신을 탑재한 웹 브라우저로 전체 전송 후 구동 > 안씀
    * Servlet
      + 서버의 요청 > 응답으로 결과값만 보내주는 구조
      + .java을 컴파일한 .class형태 
    * JSP
      + 기본은 html + 부분적 java코드3
  
  - JSP vs Servlet
    서블릿 | JSP
    -- | --
    자바 코드 안에서 전체 html페이지를 생성 | html 코드 안에서 필요한 부분만 자바 코드를 스크립트 형태로 추가
    변수 선언 및 초기화가 반드시 선행되어야 함 | 자주 쓰이는 기능을 내장 객체로 제공하여 즉시 사용 가능
    컨트롤로를 만들 때 사용 | 처리된 결과를 보여주는 view를 만들 때 사용

  - 현재 구조
    * 브라우저 <-> 웹 서버 <-> 웹 컨테이너(서블릿 + JSP엔진)
      + 웹서버(정적페이지)
      + 웹 컨테이너(동적 페이지 생성)

2. JSP 파일 기본 구조
  - 지시어
    * jsp > servlet 코드 변환 시 jsp 엔진에 스크립트언어 및 인코딩 방식 등 설정
    * 종류
      + pagge 지시어 : jsp 페이지에 대한 정보 설정
      + include 지시어 : 외부 파일을 현재 jsp페이지에 포함시킴
      + taglib 지시어 : 표현 언어에서 사용할 자바 클래스나 jstl을 선언
  - 선언부 스크립트
  - 표현식 스크립트
  - 스크립틀릿

3. 지시어
  - page 지시어
    * language : 스크립트 언어 설정
    * contentType : 문서타입설정 및 캐릭터 셋 설정
    * pageEncoding : 인코딩 방식 설정
    * import : java.lang 패키지에 속하지 않는 클래스를 가져오기 위함
    * errorPage, isErrorPagge : 실행 도중 에러가 발생하면 'HTTP Status 500'에러 표시
    * trimDirectiveWhitespaces : 지시어로 인한 불필요한 공백 제거
    * buffer, autoFlush 
      + 출력한 내용을 버퍼에 담아 일정량 이상되면 전송
      + 버퍼가 모두 채워지면 처리방법
  
  - include 지시어
    * 반복되는 부분을 별도의 파일에 작성해두고 필요한 페이지에 include 지시어로 포함

  - taglib 지시어
    * EL에서 자바 클래스의 메서도ㅡ 호출하거나 JSTL(JSP 표준 태그 라이브러리)을 사용하기 위한 지시어

4. 스크립트 요소 
  - 선언부
    * 스크립틀릿이나 표현식에서 사용할 멤버 변수나 메서드를 선언
  
  - 스크립틀릿
    * jsp페이지가 요청 받으면 실행 돼야 할 자바 코드를 작성하는 여역

  - 표현식
    * 상수, 변수, 연산자를 사용한 수식, 메소드 호출


## chapter 2 내장 객체

1. 내장 객체
  - 특징
    * 컨테이너가 미리 선언해 놓은 참조 변수를 이용해 사용
    * 객체생성없이 각 내장 객체 메소드 사용가능
    * 스크립틀릿과 표현식에서만 사용
    * 선언부는 매개변수로 전달받아 사용

2. 내장 객체 종류
  - Requset : 전송한 요청 정보를 담고 있는 객체
    * 클라이언트와 서버의 환경정보 읽기
      + getMethod() : get/post 전송방식 반환
      + getRequestURL() / getRequestURI() : 요청 주소 반환
      + getRemoteAddr() : client IP 주소 반환
      + getQueryString() : 매개변수 전달을 위한 쿼리스트링 반환
      + getParameter() : 메소드 키값을 인수
    * 클라이언트의 요청 매개변수 읽기
      + post방식인 경우 UTF-8 인코딩 설정
      + getParameter() : 전송값이 하나인 경우
      + getParameterValues() : 전송값이 여러개 인경우 
    * HTTP 요청 헤더 정보 읽기
      + getHeaderNames() : 모든 요청 헤더의 이름을 반환
      + user-agent : 웹브라우저 종류를 식별
      + referer : 링크를 통해 다른 사이트로 방문 시 남는 기록 
      + cookie : 쿠키도 확인가능

  - Response : client의 요청에 대한 응답 정보를 저장
    * 주요 메소드
      + setContentType(String) : MIME타입 지정, 인코딩 지정 
      + getCharacterEncoding() : 응답 내용 인코뎅 형태 반환
      + addCookie(Cookie) : 응답에 지정한 쿠키 저장
      + containsHeader(header) : header를 포함여부 검사
      + setHeader(name, value) :  name 헤더값을 value로 지정
      + setDateHeader(name, date) : name 헤더값을 long date 로 지정
      + ddHeader(name, value) : name 헤더값을 string형 value인 헤더 추가
      + addIntHeader(name, value) name값이 int value 헤더 추가
      + addDateHeader(name, date) name값이 long date 헤더 추가
      + encodeRedirectURL(url) : 세션정보를 포함하기 위해 url 인코딩
      + encodeURL(name) : 세선졍보를 포함하고 있는 링크에서 사용할 url 인코딩
      + sendRedirect(url) 웹 서버가 웹 브라우저에게 지정한 url로 자동이동

  - Out : JSP 페이지에 출력할 내용을 담는 출력 스트림
    * 웹 브라우저에 변수 등의 값을 출력할 때 주로 사용
    * 버퍼 사용, 출력되는 모든정보를 버퍼에 저장 후 웹 브라우저 출력

  - Application : 웹 애플리케이션 관련 컨텍스트 정보를 저장
    * 웹 앱당 하나만 생성 모든 JSP 페이지에 접근 가능
    * web.xml에 설정한 컨텍스트 초기화 매개변수를 읽어오고 폴더의 물리적 경로 찾기
    * 주요 메소드
      + getInitParamter() : web.xml에 설정한 초기화 매개변수 읽기
      * getRealPath() : 현재 작성중인 폴더의 물리적 경로를 반환

  - Exception : 예외가 발생한 경우에 사용
    * 에러가 발생했을 때 에러별로 출력할 페이지를 분기하는 법
    * 에러코드
      + 404 : 경로명이나 파일명이 제대로 입력되었는지 확인
      + 405 : doGet(), doPose()메서드가 오버라이딩확인
      + 500 : 개발중인 코드의 에러
    * 에러 발생시 코드마다 web.xml에 출력 페이지 설정

  - Session : 웹 브라우저 정보를 유지하기 위한 세션 정보를 저장
  - Page : JSP  페이지를 구현한 자바 클래스의 인스턴스
  - PageContext : JSP 페이지에 대한 정보를 저장
  - Config : JSP 페이지에 대한 설정 정보 저장


## chatper 3 내장 객체의 영역
  - 내장 객체의 영역 개념 
    * 각 객체가 저장되는 메모리의 유효기간
      + page : 동일한 페이지에서만 공유 
      + request : 하나의 요청에 의해 포워드된 페이지까지 공유
      + session : 클라이언트 접속 후 웹 브라우저 종료시
      + application : 앱 종료시 
    * 영역이 제공하는 주요 메소드
      + void setAttribute(String name, Object value)
      + Object getAttribute(String name)
      + void removeAttribute(String name)
  


------------------
jdk 8 이상
이클립스 설치
  - 이클립스 내 utf-8 설정
    * general > workspace > utf-8
    * web > jsp file > utf-8

web server
  : 초창기 웹서버는  html, js, css등 정적 데이터만 처리

web application server
  : jsp, asp, php등 동적 데이터 처리
  ex. tomcat IIS zeus
시간이 지나면서 was에 웹서버가 통합됨
업체에 따라서 web server와 was를 분리해서 운영하는 경우도 있음.

----------------------------
코드 분리

1.초기에는 코드분리없이 개발
2.UI와 로직을 분리
  -> 디자이너와 개발자의 협업에 유리
3.데이터를분리
  ->데이터처리가 명확해지고 유지보수에 유리

Model : 데이터
View : UI
Controller : 로직

코드분리는 생산성 측면에서 계속 이슈

----------------------------
개발자 입장에서 고도화

1.실행속도
2.생산성향삭
  -개발비용절감
  -유지보수절감

OBP(Object Based Programming)
처럼 내장 객체 제공
  -> javascript, visual Basic

---------------------------------------
packet의 header
  전송되는 packet에 대한 여러 정보를 가지고 있음

referer
  : 현재 페이지로 오기 저 ㄴ이전 페이지 주소를 저장하는객체
  -> 허락 받지 않은 접근을 방지할 때 사용
  b.jsp의 이전 페이지가 반드시 a.jsp이어야 할 경우 referer 값을 확인해서 처리

---------------------------------------

application : 모든 사용자 / 모든 페이지
session : 각 사용자 / 모든 페이지
request : 각 사용자 개인 / 현재 페이지 / 다른 페이지 넘길 수 있음
page : 각 사용자 개인 / 현재 페이지

--------------------------

Context
  사전적 의미는 "문맥"
 programming에서는 관련된 사항, 정보, 데이터 등의 의미

  프로젝트가 갑자기 실행이 안될 때
  workspace .metadata를 삭제하면 workspace가 초기화됨

  이클립스 종료
  .metadata 삭제
  이클립스 재실행
  톰캣설정
  기존 프로젝트 import

-------------------------------------

Bean
  : jsp DTO 역할을 하는 class객체
Enterprise Java Bean
  : java에서 Bean은 MS에서 Component에 해당
CBD
  : Component는 컴파일러 형태로 제공되는 코드부품
  -> 대기업에서 주로 사용