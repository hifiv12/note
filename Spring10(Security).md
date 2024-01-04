## 스프링 웹 시큐리티
  - Authentication > 인증 로그인 방법 
  - Authorization > 인가, 관리자 일반회원

  ROLE-ADMIN
  ROLE-MEMBER
  ROLE-USER
-------------------------

1.로그인
->로그인 폼 제공: 커스터마이징필요
->로그인 후 세션 Attribute에 값을 저장/확인 제공

2.암호화
-> 비밀번호암호화 제공

3.csrf토큰
->csrf토큰 제공

등등 보안 관련된 코드 제공

-------------

시큐리티 기본 설정
1.로그인 주소
2.id는 username, pw는 password
3.처음부터 로그인 하면'/'로 이동
4.특정 url에 접근하려다가 로그인화면으로 redirect된 후 로그인하면 원래 접근하려했던 url로 이동함
5.csrf token이 필요
->get방식을 제외한 post,put,delete방식으로 처리할 때
front에서 controller로 csrf token전달 필요
6.role이 여러개라고 설정된
->ROLE_MEMBER와 ROLE_ADMIN 두개 이상 역할 부여 가능

*Member테이블과 Authorities테이블이 필요
->ROLE이름은 정해져 있음. ROLE_USER, ROLE_MEMBER, ROLE_MANAGER, ROLE_ADMIN

csrf토큰 구현방법
1.controller에 접근하면 csrf토근을 생성
2.csrf토큰을 session attribute에 저장
3.csrf토큰을 view page로 전달
4.view page 에서 csrf토큰을 받아서 다시 controller로 전달
5.2번, 4번dml csrf토큰값이 일치하는지 확인, 일치하지 않으면 로그인 페이지나 에러페이지로 보냄
->security는 자동제공