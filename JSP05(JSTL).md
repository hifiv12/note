## chapter 11 jstl
  - JSTL (Java Standard Tag Library)
    * scriptlet없이 변수,조건,반복문 등을 처리해주는 태그, 코드가 간결함
  
  - 태그 종류

    종류 | 기능 | 접두어 |  URI
    -- | -- | -- | --
    Core | 변수 선언 / 조건문 /반복문 / URL 처리 | c | http://java.sun.com/jsp/jstl/core
    Formatting | 숫자, 날짜, 시간 포맷 지정 | fmt | http://java.sun.com/jsp/jstl/fmt
    XML | XML 파싱 | x | http://java.sun.com/jsp/jstl/xml
    Function | 컬렉션, 문자열 처리 | fn | http://java.sun.com/jsp/jstl/functions
    SQL | 데이터베이스 연결 및 쿼리 실행 | sql | http://java.sun.com/jsp/jstl/sql

  - 사용 설정
    * jsp파일 상단에 taglib 지시어 사용
      * 접두어와 uri 명시
      * ex <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
    * JSTL은 확장태그 -> 별도의 라이브러리가 필요
      * 각 프로젝트의 WEB-INF/lib/jstl-1.2.jar 필요
    
  - Core tag
    * 종류

      태그명 | 기능
      -- | --
      set | 변수 설정
      remove | 설정한 변수 제거
      if | 단일 조건문 > else문이 없음
      choose | 다중 조건문 > when~otherwise
      forEach | 반복문 처리
      forTokens | 구분자로 분리된 각각의 토큰을 처리
      import | 외부 페이지 삽입
      redirect | 지정한 경로로 이동
      url | 경로를 설정할 때 사용
      out | 내용을 출력할 때 사용
      catch | 예외 처리에 사용
    
    * <c:set> props
      + var : 변수명 설정
      + value : 변수 할당값
      + scope : 영역 지정 > default page
      + target : 자바빈즈 설정
      + property : 자바빈즈의 멤버변수 값 지정
    * <c:remove> props
      + var : 제거할 변수명
      + scope : 변수의 영역 > 지정하지 않으면 모든 영역 지정 변수 삭제
    * <c:if> props
      + test : 조건명
      + var :  조건 결과 저장할 변수명
      + scope : 영역 
    * <c:choose>, <c:when>, <c:otherwise>
      ```jsp
        <c:choose>
          <c:when test="조건1">조건1을 만족하는 경우</c:when>
          <c:when test="조건2">조건2을 만족하는 경우</c:when>
          <c:otherwise>아무 조건도 만족하지 않는 경우</c:otherwise>
        </c:choose>
      ```
    * <c:forEach> props
      + var : 변수명
      + items : 객체, 배열, 컬렉션등 지정
      + begin : 시작값
      + end : 종료값
      + step : 증감값
      + varStatus : 루프상태 저장 변수 > 향상된 for문
        - current : var에서 지정한 현재 루프의 변수값 반환 > 현재 루프 실제 요소 반환
        - index : 위와 동일 > 현재 루프의 인덱스를 표시
        - count : 실제 반복 횟수 
        - first : 루프의 처음일 떄 true
        - last : 루프의 마지막 true
    * <c:import> 
      + 외부 파일을 현재 위치에 삽입, 외부 페이지도 삽입
    * <c:redirect>
      + sendRedirect()
    * <c:url value="경로" scope="영역" var="변수">
    * <c:out value="출력할 변수" defualt="기본값" escapeXml="특수문자 처리 유무" />
    * <c:catch>실행코드</c:catch>
      +  try{} catch(){}
      + eMessage에 저장 / ArithmeticException이출력
  
  - fmt 태그
    * 국가별로 언어, 날짜, 시간, 숫자 설정
    * 접두어 설정
      + <%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
    * 태그 종류
      분류 | 태그명 | 기능
      -- | -- | --
      숫자 포맷 | formatNumber | 숫자 포맷설정
      숫자 포맷  | parseNumber | 문자열을 숫자로 포맷으로 변환 
      날짜 포맷 | foramtDate | 날짜나 시간의 포맷을 설정
      날짜 포맷 | parseDate | 문자열을 날짜 포맷으로 변환
      타임존 설정 | setTimeZone | 시간대 설정 정보를 변수에 저장
      타임존 설정 | timeZone  | 시간대를 설정
      로케일 설정 | setLocale | 통화 기호나 시간대를 설정한 지역에 맞게 표시
      로케일 설정 | requestEncoding | 요청 매개변수의 문자셋을 설정

      + <fmt:parseNumber value="파싱할 문자열" type="출력 양식" var="변수 설정" integerOnly="정수만 파싱" pattern="패턴" scope="영역" />
        - value

      + <fmt:formatDate value="출력할 날짜" type="출력 양식" var="변수 설정" dateStyle="날짜 스타일" timeStyle="시간 스타일" pattern="날짜 패턴" scope="영역" />
  
  - XML tag
    * xml 문서 처리, 파싱 및 출력 흐름 제어 등의 기능
    * <%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml"%>
    * 태그 종류
      + out
      + parse
      + forEach
      + if
      + choose
    * XML 태그는 XML 문서의 요소(element)에접근하기 위해 XPath를 사용
    * XPath는 XML 문서의 노드를 식별하고 탐색하는 역할
    * 외부 파일을 가져올 때는 한글 깨짐 현상 때문에 charEncoding 속성을 사용


## chaper 12 파입 업로드 및 다운로드
  - 준비  
    * 라이브러리 추가
      + http://servlets.com/cos/
      + cos.jar download
      + /../WebContent/WEB-INF/lib/cos.jsr

  - flow
    * 폼 작성
    * DB table 준비
    * DTO와 DAO 완성
    * 연동 후 파일 업로드

  - <form> enctype props
    * application/x-www-form-urlencoded : 전송전 모든 문자 인코딩 기본값 
    * multipart/form-data : 모든 문자를 인코딩 안함 > 파일을 전송 할 때 사용
    * text/plain : 공백 문자만 "+" 기호로 변환 나머지는 문자는 인코딩 안함
  
  - Multipartrequest class
    * param
      + HttpServletRequest request 
      + String saveDirectory 
      + int maxPostSize
      + String encoding

  
---------------------------------
multipart/form-data
  : 웹에서 form 기반 전송 방식