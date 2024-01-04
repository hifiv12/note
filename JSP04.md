## chapter 09
  - 게시판에 페이징 기능 넣기
    * BoardPage
    * BaordDAO
    * List.jsp

## chapter 10 표현언어
  - 개념 
    * 표현 언어(Expression Language, EL) : 변수의 값을 출력할 때 사용하는 스크립트 언어
  
  - 특징
    * 간결한 사용법
    * 예외와 형변환에 관대
    * 전송된 폼값이나 객체 읽기 가능
    * 컬렉션을 쉽게 사용
    * 연산자 사용가능
    * 메서드를 호출할 수 있는 기능

  - 기능
    * JSP 내장 객체의 영역에 담긴 속성 사용 가능
    * 산술, 비교, 논리 연산 가능
    * 클래스에 정의된 메소드 호출가능
    * EL 객체를 통해 JSP와 동일한 기능 수행
  
  - 기본 사용법
    * ${ 속성 }
      + 속성 : 영역에 저장된 속성 
      + html, css, js 어디에든 사용 가능
      + jsp 스크립트 요소는 사용불가
    * 객체 표현
      + ${ param.name }
      + ${ param["name"] }
      + ${ param['name'] }
      + 속성에 특수기호나 한글 포함 -> 대괄호만 사용

  - 내장 객체
    * pageScope
    * requestScope
    * sessionScope
    * applicationScope
    * cookie
    * header
    * headerValues
    * initParam
    * pageContext
  
  - 컬렉션
    * LIST
    * Map

  - 연산
    * 할당 연산
    * 산술 연산
    * 비교 연산
    * 논리 연산
    * empty연산
    * null 연산

  - TLD(Tag Library Descriptor)
    * 사용자 정의 태그나 JSTL 태그들을 설정하기 위한 XML 파일
    * 확장자는 XML이 아닌 tld WEB-INF 폴더에 작성



-----------------------------------------

el

parameter를 받기

attribute를 받기

---------------------

custom tag library만들기
1.class
2.class ~.tdl
3.

action tag
el
jstl로 사용해야됨