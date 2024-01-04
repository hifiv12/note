## Setting
  - jdk 17
    * mac : asdf로 설치, 로컬 & 글로벌 버전 관리
    * win : jdk installer로 설치 하고 JAVA_HOME 을 script로 관리해서 버전 변경
  - vscode
    * extension
      + Extension Pack For Java
      + Spring Boot Extension Pack
      + Lombok Annotations Support
    * settings : Compact Folders -> 트리 구조로 보여줌, 자바의 패키지 구조를 트리로 봄 
  - start.springintializr.io 
    * Project : Gradle - Grooby
    * Language : JAva
    * Spring Boot : 3.0.10
    * Group : com.mysite
    * aftifact : sbb
    * name : sbb
    * Packaging : Jar
    * Java : 17
    * Dependencies : Spring Web

## Hello Spring Boot
  - Spring Boot Devtools
    * 서버 재시작 없이 클래스 변경시 서버가 자동으로 재기동
    * build.gralde.dependencies 
      + developmentOnly 'org.springframework.boot:spring-boot-devtools'
        - developmentOnly : 개발환경에만 적용되는 설정, 운영환경에 배포되는 jar, war 파일에 포함되지 않는 라이브러리