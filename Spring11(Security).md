  - 로그인 성공과 AuthenticationSuccessHandler
    * 로그인 성공 후 특정 URI로 이동하거나 쿠키 처리 등의 추가적인 작업
    * org.zerock.security.CustomLoginSuccessHandler (class)
    * security-context.xml
      + bean 생성
      + security-form-login
  
  - 접근 제한 메세지의 처리
    * org.zerock.security.CustomAccessDeniedHanlder
      + 접근이 거부 되었을 때 처리 방법
      + AccessDeniedHandler 상속
      + sendRedirect를 통해 에러페이지 이동
    * security-context.xml
      + security:access-denied-handler
      + bean 생성

  - 로그아웃 처리와 LogoutSuccessHandler
    * security-context.xml
      + security:logout
    * view 로그아웃 페이지

  - JDBC를 이용하는 간편 인증/권한 처리
    * 회원 테이블의 설계
     + sql 작성
    * Security-context 설정
      + security:jdbc-user-service
    * PasswordEncoder 설정
      + spring 4까진 별도의 PasswordEncoder를 이용하고 싶지 않으면 NoOpPasswordEncoder를 이용해서 처리 5부터는 deprecated
      + 암호화를 피하고 싶다면 PasswordEncoder를 직접 구현
      + security:password-encoder
      + bean 생성
      + org.zerock.security.CustomNoOpPasswordEncoder
        - PasswordEncoder 상속
    * sql tbl_member, tbl_member_auth 테이블 추가

  - BCryptPasswordEncoder
    * bcrypt는 태생 자체가 패스워드를 저장하는 용도로 설계된 해시 함수
    * 특정 문자열을 암호화, 체크하는쪽은 암호회돤 패스워드가 가능한 패스워드인지만 확인
    * bean 생성
    * security:password-encoder 추가

  - 쿼리를 이용하는 인증

  - 커스텀 UserDetailsService 활용 
    * 사용자가 원하는 방식으로 인가/인증 처리를 하기 위해 
    * 직접 UserDetailsService 인터페이스를 구현해서 처리











-------------------------------------

bean -> 인스턴스 

암호화
  -> 평문을 암호화 알고리즘을 사용해서 암호화된 문자열로 만드는것
복호화
  -> 암호화된 문자열을 원래대로 평문으로 되돌리는 것

암호화 알고리즘
  -> 암호화/복호화 모두 제공하는 알고리즘
  -> 암호화만 제공하는 알고리즘
    ** 비밀번호암호화에 사용 > Bcrypt알고리즘

암호화 할 때 key를 사용하는 경우는
복호화 할 때 key가 필요

IBatis -> MyBatis

join 했을 때 결과 처리

1.Map
  -> 컬렴명이 Map의 Key로 생성됨
  -> VO를 사용 안하므로 Model을 활용하지 않게 됨
2.VO
  -> join 컬럼을 모두 저장하기 위한 VO를 새로 만들어서 사용
  -> 조인 할 때 마다 VO를 생성해야 함

3.MyBatis에서 제공하는 resultMap을 사용
  -> Join 컬럼을 모두 저장하기 위한 VO를 안만들어도 됨
  -> VO 사용하므로 Model활용
  -> syntax 가 복잡함

mapper.xml
mapper interface
service

principal
  * 로그인한 사용자의 정보
