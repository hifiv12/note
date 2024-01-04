- 조회 페이지와 영화 리뷰
  * 영화를 조회하는 경우, 여러영화의 이미지들이 같이 나오므로 별도의 과정이 필요
  * MovieController와 read.html
  
- Ajax로 영화 리뷰 처리
  * 모달 창을 이용해서 리뷰 추가
  * 사용자는 감상과 별점(점수)를 부여
  * 댓글 추가 후에는 조회 URL을 다시 호출해서 모든결과를 반영하는 방식으로 구성
  * 추가 후 필요부분만 갱신하는 방법도 고려

- ReviewService / ReviewDTO / Review
  * ReviewService
    + 특정한 영화의 모든 리뷰를 가져오는 기능
    + 새로운 영화 리뷰를 등록하느 ㄴ기능
    + 특정 영화 리뷰를 수정하는 기능
    + 특정 영화 리뷰를 삭제하는 기능
- ReviewController

- read.html에서 리뷰 처리
  * 2개의 모달창을 사용 - 하나는 이미지 뷰어용
  * 별점 처리 라이브러리
  * 리뷰 등록은 Ajax로 post방식으로 json문자열 전송
  * 리뷰 리스트는 페이지가 보여질 때 자동으로 호출하도록 작성
  * 특정 리뷰를 선택하면 모달 창의 내용과 버튼들을 조정
  * 리뷰의 수정은 PUT 방식
  * 리뷰의 삭제는 DELETE 방식
  * 섬네일을 클릭하면 원본 이미지를 모달 창에 추가해서 보여주는 방식을 구현

- 현재까지의 문제점
  * 리뷰 댓글을 달때 이메일 인증이 아닌 데이터베이스에 mno 값으로 인증해야된다. > 사용자 친화적이 아님
  * 리뷰 댓글의 리플의 구분감이 없음
  * 수정도 쉽게 이뤄짐 인증절차 X
  * read 페이지에서 리스트로 가는 버튼이 존재하지 않는다.

## Spring Boot and Spring Security 
  - 서론
    * 스프링 시큐리티는 기본적으로 HttpSession방식
    * 전통적인 id/pw 기반의 로그인 처리
    * jpa를 이용하는 커스텀 로그인 처리
    * thymeleaf에서 로그인 정보 활용하기
  
  - 프로젝트 생성
    * 프로젝트 생성시에 security 항목을 추가
    * 프로젝트 실행시 임시 패스워드 확인
      + 계정명은 user
      + 32b8c118-3649-4a5e-846f-ed2bf3a2ef95

  - 시큐리티 설정 클래스 작성
    * SecurityConfig 클래스 추가
    * SampleController 클래스 추가
  
  - 스프링 시큐리티 용어와 흐름
    * 기본적으로 필터를 이용해서 동작
    * 필터와 AuthenticationManager 등의 객체를 이용해서 동작
    * 필터와 필터 체이닝
  
  - 인증을 위한 AuthenticationManager
    * 인증 매니저
    * 내부적으로 AuthenticationProvider와 연게되어 동작
  
  - PasswordEncoder
    * 스프링 부트 2.0부터 반드시 필요
    * 인터페이스이므로 구현하거나 구현된 클래스 이용
    * BcryptPasswordEncoder
      + 패스워드 암호화 전용
      + 동일한 메세지도 매번 다르게 암호화 생성
      + 복호화 불가
      + 올바르게 암호화 된 것인지만 확인
  
  - AuthenticationManager 설정
    * 우선은 단순히 로그인이 가능하도록 설정하고 추후에 변경
    * localhost:8082/login 으로 동작확인
  
  - CSRF 설정
    * Cross Site Request Forgery 크로스 사이트 요청 위조
    * 스프링 시큐리티를 적용하면 기본적으로 CSRF방지를 위한 토큰이 사용
    * GET방식을 제외한 모든 요청에 대해서 CSRF토큰이 필수적으로 필요
    * csrf().disable()을 통해서 비활성화 가능
    * CSRF토큰이 비활성화 되면?
  
  - 프로젝트를 위한 JPA 처리
    * 회원정보
      + 이메일
      + 패스워드
      + 이름
      + 소셜 가입 여부
      + 등록/수정일
    * 권한
      + USER
      + MANAGER
      + ADMIN
  
  - Repository와 더미데이터 추가
    * ClubMember USER(1~80), USER/MANAGER(81~90), USER/MANAGER/ADMIN(91~100)을 가지도록 설정
  
  - 시큐리티를 위한 UserDetailsService
    * 개발자가 원하는 방식으로 로그인을 처리하기 위해서 구현하는 인터페이스
    * User라는 용어는 키워드 처럼 사용됨
    * username이 실제로는 ID에 해당
    * username/password가 동시에 사용되는 방식이 아니므로 주의
    * 인증이 끝나면 인가처리
    * loadByUsername() : username이라는 회원 아이디로 UserDetails타입의 객체를 반환
    * UserDetail 인터페이스를 이용해서 구할 수 있는 데이터
      + getAuthorities() : 사용자가 가지는 권한에 대한 정보
      + getPassword() : 인증을 마무리 하기 위한 패스워드 정보
      + getUsername() : 인증에 필요한 아이디와 같은 정보
      + 계정 만료 여부 : 더이상 사용이 불가능한 계정인지 알 수 있는 정보
      + 계정 잠김 여부 : 현재 계정의 잠김 여부
    * 기존 구조에서 UserDetails를 처리하는방식
      + 기존의 DTO 클래스에 UserDetails 인터페이스를 구현하는 방법
      + DTO와 같은 개념으로 별도의 클래스를 구성하고 이를 활용하는 방법
    * org.springframework.security.core.userdetails 를 상속하는 DTO
  
  - UserDetailsService 구현
  - SecurityConfig 수정
    * ClubUserDetailsService가 빈으로 등록되므로 별도의 설정없이 기존의 AuthenticationManagerBuilder를 이용하는 메서드는 필요없음
    * ClubMemberRepository의 메서드에 @Param으로 jpql 파라미터와 연결
    * build.gradle
      + thymeleaf-extras-springsecurity5 버전을 지정하지 않고 주입해야 오류가 안남
      + 는 refresh로 해결
    
  - Thymeleaf를 이용한 사용자 정보 출력
    * member.html
    * sec:authorize 

## 스프링 시큐리티 소셜 로그인
  - 개념
    * 인증에 대한 처리를 제 3의 존재(소셜 서비스등)를 이용하는 방식
    * 기존과 달리 별도의 회원 가입이 필요하지 않음
    * OAuth/OAuth2.0 기반으로 동작
