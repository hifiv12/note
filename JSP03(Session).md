  - prepareStatement vs Statement

## chapter 06 세션(Session)
  - 개념 : 클라이언트가 서버에 접속해 있는 동안 그 상태를 유지하는 것이 목적
    * 대게 로그인-아웃에 사용함

  - 세션 설정, 확인, 삭제
    * 유지 시간 설정
      + web.xml에서 설정

        ```xml
          <session-config>
            <session-timeout>20</session-timeout>
          </session-config>
        ```

      + jsp에서 설정

        ```jsp
          <% 
            session.setMaxInactiveInterval(1800);
          %>
        ```
      
      + 서버는 글로벌 jsp코드는 로컬 -> 우선순위는 jsp 코드가 높다.
    * 설정값 확인
    * 세션 삭제


  - 쿠키 vs 세션
    -- | 쿠키 | 세션
    -- | -- | --
    저장 위치/형식 | 클라이언트 PC에 text로 저장 | 서버에 Object 타입으로 저장
    보안 | 클아이언트에 저장되므로 보안에 취약 | 서버에 저장되므로 보안에 안전
    자원/속도 | 서버 자원을 사용하지 않으므로 세션보다 | 서버 자원을 사용하므로 쿠키보다 느림
    용량 | 용량의 제한이 있음 | 서버가 허용하는 한 제한이 없음 
    유지 시간 | 쿠키 생성 시 설정, 단 설정된 시간이 경과되면 무조건삭제 | 서버의 web.xml에서 설정. 설정된 시간 내라도 동작이 있다면 삭제되지 않고 유지
 

 ## chapter 07 액션 태그
  - 개념 
    * JSP 표준 태그, 페이지 이동 제어 및 자바빈 생성 시 사용

  - 특징
    * XML 문법
    * scriptlet

  - 지시어와 액션태그의 차이점
    * 액션태그 <jsp:???? asdf="">
    * 표현식 사용 가능
    * 실행의 흐름에 포함시킬 페이지로 이동 시킨 후 실행한 결과를 현재 페이지에 포함 지시어는 반대
    * 포함 시킨 파일에서 생성한 변수 사용 불가
    * 페이지 영역 공유 불가
    * 공유됨

  - <jsp:include>
    * 특정 페이지를 현재 페이지에 포함시킬 때 사용
    * include 지시어와 비슷한 기능이지만 동작 방식에 차이가 있음
  - <jsp:forward>
    * 요청을 전달하는 포워드에 사용
  - <jsp:useBean> 
    * <jsp:setProperty>
    * <jsp:getProperty>
    * 자바 빈즈를 생성하거나 값을 설정 및 출력
    * asterisk를 사용하면 전송되는 폼값을 한 번에 받음
  - <jsp:param>
    * 인클루드나 포워드 시 매개변수를 넘길 때 
  

-----------------------------------------------------

로그인 프로세스
1.id,pw를 form에 입력, 서버에 전송
2.id,pw가 일치하면 session attribute에 값을 저장
  ->일반적으로 id를 저장
3.main페이지로 이동
4.main페이지에서 로긴 여부를 2번이나 저장한 attribute값 존재여부로 판단
5.로그아웃할 때는 sessio attribute 모두 삭제.

** 스프링에서는 spring security가 이작업을 대신 수행 **

------

패턴 : 개발, 규칙 방법론

MVC패턴 
Model - 데이터 = class로 구현
View - UI : JSP로 구현
Controller - 로직 : servlet으로 구현

View를 담당하는 JSP에서 가급적 <%...%> scriptlet를 사용하지 않는다.
대신 action tag 

crud history

dao

MyBatis
mapper

JPA
repository