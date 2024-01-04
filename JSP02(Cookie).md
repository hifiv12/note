  - 데이터 전송 객체(DTO)
    * 데이터를 저장하거나 전송하는 객체, 순수하게 데이터만 담고 값 객체라고도 부름
    * 자바빈즈(Java Beans)규약에 따라 작성
      + 기본 패키지 이외의 패키지에 속해야 함'
      + 멤버 변수(속성)의 접근 지정자는 private
      + 멤버 변수 접근 가능한 getter/setter 메소드 필요
      + getter/setter 메소드 public 지정
      + javaResource/src > new > Person class(DTO) 작성
  
  - page 영역
    * 클라이언의 요청을 처리하는 데 관여하는 JSP 페이지 마다 하나씩 생성
    * 각 JSP페이지는 page영역을 사용하기 위해 pageContext 객체를 할당
    * 페이지를 벗어나면 소멸

  - request 영역
    * 하나의 요청에 대한 응답이 완료될 때 소멸하게 되므로 page영역보다는 접근 범위가 조금 더 넓다.
    * forward 된 페이지에도 넘겨줄 수 있다.
    * 새로운 페이지 요청 시 소멸

  - session 영역
    * 클라이언트가 서버에 접속해 있는 상태 혹은 단위, 주로 회원인증 후 로그인 상태를 유지하는 처리에 사용
    * 웹 브라우저를 닫을 때 까지 공유

  - Application 영역
    * 단 하나의 application 객체만 생성하고, 클라이언트가 요청하는 모든 페이지에 application 객체를 공유
    * 웹서버 시작할때 생성, 웹 서버 내릴 때 삭제

## 쿠키(Cookie)
  - 개념
    * 클라이언트의 상태 정보를 유지하기 위한 기술
    * 키:값 형태로 저장, 다음 요청시 저장된 쿠키를 함께 웹서버로 전송
    * 쿠키 표준
      + 3000개까지
      + 쿠키 하나 최대 크기 4096byte
      + 하나의 호스트나 도메인에서 최대 50개
      + 브라우저마자 상이하나 최대 용량은 1.2Mb

  - 작동방식 
    1. 클라이언트가 서버에 요청(처음 방문)
    2. 서버가 쿠키를 생성하여 http 응답 헤더에 클라이언트에 전송
    3. 클라이언트가 쿠키를 받아 저장
    4. 클라이언트가 다음번의 요청 시 저장해둔 쿠키를 http 요청 헤더로 서버에 전송
    5. 서버는 쿠키의 정보를 읽어 필요한 작업을 수행

  - 속성과 API
    * properties
      + name : 쿠키 이름
      + value : 저장할 데이터
      + domain : 적용할 도메인
      + path : 적용할 경로
      + max age : 유지 시간
    * set method
      + void setValue(String value) : 데이터 설정
      + void setDomain(String domain) : 도메인 설정
      + void setPath(String path) : 경로 지정
      + void setMaxAge(int expire_seconds) : 초단위 설정
    * constructor
      + new Cookie(String name, String value) : 생성자
    * get method
      + getName()
      + getValue()
      + getDomain()
      + getPath()
      + getMaxAge()

  - 레이어 팝업창 제어
    * 쿠기 없이 기본 기능 구현
    * 쿠키를 이용해 상태 정보 유지


------------------------------------
session Attribute
  :모든 접속자마다 개별적으로 서버 메모리에 생성됨
  -> 로그인 작업 처럼 중요한 부분이외에는 사용안함
  -> 로그인 작업 이외에는 주로 Cookie를 사용
  ex. 자동 로그인, 임시장바구니 등등

Application Attribute
  :모든 접속자가 공용으로 사용
  -> 변경되면 모든 접속자에게 영향을 줌

  :접속자 컴퓨터에 생성됨
  -> 서버의 부담을 줄일 수 있음
  -> 로그인 작업 이외에는 주로 Cookie를 사용
  ex. 자동 로그인, 임시장바구니등등
  -> 공용 pc에서는 쿠키사용 자제
  -> setMaxAge()로 유지기간을 설정안하면 브라우저에서 접속중일 때만 유지
브라우저에서 접속중일때만 유지
브라우저가 종료되면 소멸(메모리 쿠키)

Connection Pool
  : Connection 객체를 미리 만들어서 Pool에 넣어 놓고,
  접속할 때 Pool에서 Connection 객체를 꺼내서 사용하다가
  접속이 끊어질 때 Conection객체를 Pool에 다시 반납하는 개념
  -> 동시 접속자가 많을 때 성능개선

Spring, Spring Boot에서 Hikari CP