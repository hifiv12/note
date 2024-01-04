  - OAuth
    * Open Authorization

  - 설정방법
    * 구글 개발자 플랫폼
    * 프로젝트 생성
    * API 및 서비스 사용 설정
    * Oauth 동의 화면 
      + 외부
    * 테스트 사용자
      + 이메일 2개
    * 사용자 인증 정보
      + OAuth클라이언트 ID 만들기
      + json다운로드
    * application.properties
      + 정보입력
    * SecurityConfig 
      + http.oauth2Login()

  - 프로젝트 연동
    * ClubOAuthUserDetailsService
    * 사용자 이메일 추출

  - 이메일을 이용한 회원 가입 처리
    * ClubMemberRepository와 PasswordEncoder를 주입해서 회원 가입

  - OAuth2User 타입
    * 화면에서 정상적으로 회원 정보를 처리하기 위해서는 ClubMemberDTO타입으로 변환이 필요
    * ClubUserDetailsService
      + ClubAuthMemterDTO 변경 필요

  - 자동 회원 가입의 후처리
    * AuthenticationSuccessHalder 를 지정해서 인증 성공 후 처리를 지정
    * 소셜 회원 가입후에 일반 회원으로 전환할 수 있도록 옵션을 제공

  - Remember me 와 @PreAuthorize
    * HttpCookie를 이용하는 자동 로그인 방식
    * 쿠키의 경우 유효시간을 이용해서 세션이 종료된 후에도 사용가능
    * SecurityConfig클래스를 이용해서 @Override 설정

  - @PreAuthorize
    * 어노테이션을 이용한 시큐리티 접근제한 적용
    * 설정 단계
      + @EnableGolobalMethodSecurity의 적용
      + 접근 제한이 필요한 컨트롤러의 메서드에 @PreAuthorize 적용

---------------------------------------

n : 1 문제





-------------------------------

소셜 로그인 사용시 참고사항

1.자체 로그인 + 소셜 로그인 
1-1.자체회원가입제공
  -> 자체 회원가입 정보와 소셜 로그인 정보가 연동
1-2.자체회원가입없이 소셜로그인을 통해서 회원가입
2.소셜로그인만 제공
