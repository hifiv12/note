## chatper 08 모델1 방식의 회원제 게시판 만들기
  - 모델 1과 2의 차이
    * 모델 1
      + jsp : view and controller
      + javaBeans : model and controller
    * 모델 2
      + servlet : controller
      + jsp : view
      + javaBeans : model
  
  - 게시판의 기능
    * 목록보기
    * 글쓰기
    * 상세보기
    * 수정하기
    * 삭제하기

  - 흐름과 권한
    * 목록 보기와 상세보기는 로그인 없이 접근가능
    * 글쓰기는 로그인 후
    * 수정과 삭제는 로그인 후 본인이 작성한 게시물
    * 로그인 시 session 내장 객체와 session 영역 사용
    * 데이터 베이스 연결을 위한 설정값은 web.xml에 저장
    * 동적쿼리 적용 PreparedStatement
    * alert 경고창, location.href 페이지 이동의 사용성

--------------------------------------------------------

게시판 목록에서 글번호를 출력하는 방법

1.virtual number
  : 가상의 글번호를 하나씩 줄여가면서 출력
  -> 보기에는 좋으나 실제 글번호가 아님
2.real number
  : 실제 글번호를 출력
  -> 보기에는 안좋으나 실제 글번호
  -> 검색에 도움이 됨
3.글번호를

---------------------------------------------------------------
## chapter 15 웹소켓으로 채팅 프로그램 만들기
  - 웹소켓
    * 웹 브라우저에서 소켓 지원
    * HTML5 이후 각 브라우저에서 적용
    * 웹소켓 서버의 구현은 애너테이션을 이용
      + ServerEndPoint
      + OnOpen
      + OnMessage
      + OnClose
      + OnError
    
  - 채팅 서버 
    * ws : WebSoket
    * 웹소켓 서버에 클라이언트가 접속 -> websoket session이 생성
    * 접속자를 구분하기 위해 websoket session id가 자동 생성
      + tomcat의 session id와 별개

## chat 16 SMTP를 활용한 이메일 전송하기
  - SMTP
  - 이메일 전송 프로그램 작성
    * 라이브러리 설치

## chaper 17 Naver search API = openAPI
-------------------------------------

웹 메일 
  : 메일을 폼에 입력해서 전송
  -> SMTP서버가 먼저 구축되어 있어야함
  -> naver나 google의 무료 smtp서버 활용

회원가입시 이메일 인증 절차
1 회원 가입 폼에 이메일 주소를 입력
2 이메일 인증 버튼 클릭
3 서버에서 이메일 인증 번호 생성, 서버쪽에 저장(session or table)
4 사용자 이메일 주소로 인증 번호 발송
5 사용자가 인증 번호 확인 후 인증번호 입력
6 입력한 인증번호 일치하면 회원가입 처리

## chaper 18 배포하기
  - war
  

----------------------------------------

클라이언트 - 서버 구조
  - 프론트엔드
    * html / css / javascript
    * angular / vues / react
  - 백엔드

백엔드 중심 개발

프론트엔드 중심 개발
  - ajax RestPul 
    + post / get / put / delete

새로운 웹 개발 트렌드
  - 자바 언어의 대안 등장
    * kotline / go / dart
      + spring boot

  - 백엔드 개발 및 운영 환경의 변화
    * 클라우드 기반의 서버 운영 보편화
    * node.js 파이썬을 이용한 서버 프로그램 개발
    * REST API 형태의 개발
    * 구글의 Firebase를 

자바 웹 개발환경
  - 서블릿 컨테이너(Web Application Server, WAS)
  - WAS가 동작 하려면 서블릿 컨테이너가 필요

spring boot에서는 embedded tomcat사용 
war에서 tomcat을 포함해서 배포
-> tomcat설치 없이 서비스 운영 가능
-> war을 업로드하면 끝

배포 프로세스
  - 데브옵스의 구성요소
    * SCM
    * CI(Continuous Integration)
    * CD(continuous Deploy)
    * CM(Confi)

------------------

물리
데이터 링크
네트워크
전송
세션
표현
응용

cloud 
  : 대기업에서 서버(WAS)+네트워크+DB를 구축하는 비용을 절감하기 위해서 자체적으로 구축하지 않고일정 비용을 내고 빌려 사용하는 개념
  -> 기존 호스팅과 다른 점은 쉽게 용량을 증설/축소가 가능

우리회사가 cloud를 도입해서 얻는 이점을 잘고려
  -> 증설/축소를 자주 해야 하는지?
  -> cloud를 전문적으로 운영할 인력은 있는지?
    대기업, 유니콘 기업은 cloud engineer팀이 별도
     전문인력이 없다면 AWS LIGHTSAIL을 추천

front end javascript framework or library

1 jQuery
  -> Back end 개발자나 publisher들이 많이 사용
  -> AJAX, DOM, Animation 작업에 편리

2 AngularJS
  -> google
  -> jQuery의 AJAX에서 생산성 향상
  model 분리
** Angular **
  -> AngularJS2.0으로 발표 > Angluar로 개명
  -> 완전히 다른 Syntax


3 ReactJS
  -> FaceBook
  -> Virtual DOM을 도입해서 자주 변경되는 컨텐츠를 반영할 때 성능 향상
  -> React Navtive를 이용하면 ReactJs로 만든 웹을 앱으로 변환 가능
  -> front end 개발자가 앱도 만들 수 있다.
  -> Component방식 개발
    ->Component는  class로 개발 -> 함수로 개발 변경
*** 우리나라에서는 프론트 엔드 개발자로 커리어를 쌓아가려면 ReactJS를 공부하는 것이 유리

4 vueJS
  -> AngularJS의 Syntax와 ReactJS의 Virtual DOM을 도입

5 vanillaSCript
순수하게 javascript만 사용하자는 개념
  -> 자바스크립트도 ajax, dom작업이 많이 편리해짐
  -> class가 도입(00p개발)
  ex> bootstrap5.0부터 only javascript만 사용


JSTL / EL
scriptlet의 구조적 문제를 해결 하기 위한 

Spring boot
thyme leaf로 많은 능력 과시

서블릿 동작 과정
접속자 마다 스레드, 세션이 만들어진다.

서블릿의 단점
  java코드와 html코드가 분리가 안됨
  디자이너와 협업이 불편
  ui를 분리해서 작업하기 불편

스프링 프레임워크로 구현
  return "userInfo"; >> userInfo.jsp로 포워딩

세션 
  * 서버 쪽에 생성되는 공간
  * 사용자마다 생성되는 공간
  * 동시에 많은 사용자 > 충분한 메모리 또는 세션 관리 대책 필요
  * 로그인 관련 작업에 주로 사용
  --------------------------------------------------------

flutter
  -> React Native 처럼 multi platform  방식
  -> android, ios, winddows
  -> 구글에서 개발
  -> React navtive보다 성능 우수
  -> 미국에서는 fultter사용자가 많아짐
