## chapter 13 Servlet
  - servlet 개념
    * jsp가 나오기전 웹 앱 개발을 위한 기술
    * 서버에서 클라이언트 요청을 받고 응답하는 역할
    * Controller 역할
    * 모든 메소드는 스레드로 동작
    * HttpServlet 클래스 상속

  - Servlet Container
    * http 요청 > 웹서버가 서블릿 컨테이너에게 요청 전달
    * 서블릿 컨테이너에서 응답> 웹서버가 http 응답함
    * 컨테이너로 톰캣 사용
      + 서블릿의 수명 주기를 관리, 요청 > 스레드 생성 및 처리
        - 인스턴스 초기화 및 응답 후 가비지 컬렉션을 통해 소멸
        - 멀티 스레딩 관리 
      + 요청 및 응답 통신 지원
        - 복잡한 통신 과정을 간단히 한 API

  - Servlet 의 동작 방식
    * mvc 패턴의 controller
    * model 2 방식 
    * 서비스 객체는 컨트롤러가 요청을 분석 한 후 호출되어 비즈니스 로직을 처리
  
  - Servlet 작성 규칙
    *  javax.servlet, javax.servlet.http, java.io 패키지를 임포트
    *  public class 서블릿클래스명 extends HttpServlet
      + public, extends HttpServlet을 반드시 명시
    * doGet(), ddoPost() 오버라이딩
      + ServletException, IOException throws 선언
      + 호출 시 매개변수는 HttpSErvletRequest, HttpServletResponse
  
  - 작성
    * 매핑
      + WEB.xml
        - 서블릿 등록한 후 해당 서블릿과 요청 URL을 매핑
        ```xml
          <servlet>
            <servlet-name>서블릿명</servlet-name>
            <servlet-class>패캐지를 포함한 서블릿 클래스명</servlet-class>
          </servlet>
          <servlet-mapping>
            <servlet-name>서블릿명</servlet-name>
          </servlet-mapping>
        ```
        - 
      + @WebSerlvet
        - 단점 : 서블릿 개수가 많아지면 클래스 찾기가 힘들어짐 > 검색방법이 없음
        - 쓸려면 > 명확한 이름 규칙을 정해야됨


## chapter 14 모델 2방식(MVC 패턴)의 자료실형 게시판 만들기

----------------------------------------------------

servlet virtual 주소 사용

MVC 패턴 규칙

1.URL주소는 Servlet에 매핑한 가상의 URL만 사용
  -> /Board/list.jsp(x)
  ex> <a href="/board/List.jsp">(x)
      <form action="regist.jsp">(x)
      location.href="/board/view.jsp?bno=10";(x)
  -> controller를 통해서 view 페이지로 이동
    forward(): 주소불변
    sendRedirect(): 주소변경
    -> spring에서는 가상 url과 같은 이름의 jsp파일로 자동 forward

2.view page(jsp)에서는 <%...%>를 거의 사용안함
  -> Action tag, EL, JSTL로 처리

3.CRUD작업에서 MODEL을 사용
  ->MODEL(데이터)가 분리 되야 함
  ->select는 return 값에 사용
  ->insert, update, delete는 paramter에 사용
  ->delete는 primary key를 parameter로 사용

* Form에 입력할 값 DTO에 저장한 후 insert처리
--> spring에서는 자동으로 dto에 데이터가 수집됨
* select한 결과를 dto에 담아서 jsp에 전달
--> mybatis에서는 select한 결과를 dto에 자동으로 저장해줌