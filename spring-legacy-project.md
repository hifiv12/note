# Spring lehacy project
  - Spring boot을 쓰기전 과거 버전
  - 주로 XML로 세팅

## install
  - jdk 11
  - STS 3.9.18
    * spring 4.0 버전부턴 legacy를 지원하지 않음(?)
    * 만약 4.0 버전을 넘기면 vscode 나 intellij로 진행
  - apach tomcat 9.0
    * spring boot는 내장

## default set
  - directory 구조
    * Deplayment Descriptor : servlet web.xml 파일 느낌
      + 배포서술자
      + Welcome 페이지 설정
      + error 페이지 설정
      + ServletContext 설정
      + Servlet/JSP mapping
      + 보안 설정
    * Spring elements
      + 스피링 구성 요쇼 및 기능(추측)
    * JAX-WS Web-service
      + Java API forXML Web Services
      + 자바 언어를 사용해 XML 기반 웹 서비스를 개발 및 실행을 위한 API 기술
    * src/main/java
      + .java 파일들이 모여 있는 곳
      + 패키지로 디렉토리를 구분해 사용
      + 스프링 구조에 맞춰 클래스 파일 작성한다면 자동적으로 MVC패턴으로 만들어짐
    * src/main/resources
      + 자바 클래스에서 사용하는 리소스 보관 장소
      + DB 연결을 위한 자원, DI를 위한 xml파일 
    * src/test/java
    * JRE System Library
    * Maven Dependencies
    * src
    * target
    * pom.xml
