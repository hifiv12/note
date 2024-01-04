# part 1

## STS 3 default Setting for jdk

  - java build path
    * project > properties > java build path > libraries > JRE system library > edit > alternative jre : jdk 11
  - java Compiler
    * java > 11
  - project Facets
    * java > 11
    * runtime tap > apach tomcat v9.0

## 프로젝트시 충돌 후 통상 해결방법
  - maven
    * project 우클릭 > maven > update project 
    * 가끔가다가 비정상적으로 작동 할 때?
  - tomcat 
    * clean : 톰캣이 가지고 있는 정보를 삭제해
    * clean work directory : 2번째
    * 다 안되면 톰캣 삭제 후 다시 세팅  
  - maven defendencies
    * C:\Users\y\.m2 > 삭제 하더라도
    * maven이 체크 해서 다시 library 다운로드
  
## setting
  - install
    * jdk 1.8
      + 환경변수
    * sts or eclipse 
    * tomcat 9.0

## chater 02 스프링 특징과 의존성 투입
  - 의존성 주입(Dependency Injection)
    * 객체를 자동으로 생성해서 주입
    * 마틴 파울러
    * 외부에서 설정을 통해서 객체간의 연결하는 패턴
    * 실행시 의존 관계가 완성되는방식
  
  - Heavy / LightWeight FrameWork
    * 2000년대 초반 
      + EJB (Enterprise Java Beans)
        - 대기업을 위한 개발 방식
        - Bean(Component)를 먼저 만들어서 Bean을 결합해서 프로그램을 완성하는 방식
        - 개발난이도 상승 및 개발기간 길어짐
        - 상용 WAS의 사용 
      + 비싼 WAS
      + 많은 것의 통합
    * 2000년대 중반
      + 빠르고 가벼운 개발 방식
      + 작은 서비스의 군집화
    * 2010년 이후
      + microservice
  
  - AOP(Aspect-Oriented-Programming)지원
    * 필요한 기능들을 모듈화, 비즈니스 로직을 가진 객체와 결합
    * cross-concern : 보안이나 로깅과 같이 시스템 여기저기서 필요한 공통적인 기능
    * AOP는 횡단 관심사를 분리, 이를 결합하는 기능이 필요
    * Sporing AOP는 Proxy 객체 생성

  - 의존성 주입 예제

  - 스프링 동작하며 생기는 일
    * root-context.xml의 설정 내용이 동작 > 필요한 인스턴스들(beans)를 생성, 의존 관계를 파악해서 주입시켜주는 방식
    * 레스토랑 클래스가 만들어지며 자동적으로 쉐프 클래스가 만들어지는 과정

  - 스프링 4.3 이후의 자동 주입
    * 기존 
      + @inject, @Autowirted, @Resource > 주입에 대한 Annotation  설정
    * 4.3
      + 단일 파라미터를 이용하는 생성자에 한해서 특정 타입의 객체를 자동으로 주입

## chapter 03 스프링과 Oracle Database 연동

  - maven으로 세팅하는법?

## MyBatis와 스프링 연동
  - 개념
    * SQL Mapping 프레임 워크
    * Spring에서 사용

  - sql 코드가 분리 > xml코드로 이동

# Part 2 
  - MVC(Model-View- Controller)
    * 대부분의 서블릿 기반 프레임워크들이 사용하는 방식
    * 데이터와 처리, 화면을 분리하는 방식
    * model 2 방식


--------------------------------------

strucs, spring같은 프레임워크의 등장으로 EJB, CBD 방식이인기가 없어짐
CBD(Component based Development)
  -> MS에서 만든 component를 활용한 개발 방식
개발방식
COmponent는 초기에는 컴파일된 부품을 의미
  -> 근래에는 특정기능을 구현한 클래스를 으미하기도 함 
  -> ReactJS의 컴포넌트

AOP(Aspect-Oriented-Programming)
  : 관점 지향 프로그래밍
Aspect
  : 공통 관심사를 지향

pom.xml에서 주입했는데 오류 난다 > scope 범위 조심

---------------------------------------------------

maven 사용
  : pom.xml에 라이브러리 등록
  -> 배포시 pom.xml 업로드. pom.xml에 등록된 라이브러리가 자동설치됨

-------------------------------------------

name space(이름 공간)
  : 자바의 package와 비슷한 역할
  ex> XML, C# 등에서 사용

-----------------------------------

단위 테스트(unit test)
  : 개발자가 자신의 코드를 직접 테스트

통합 테스트
  : 팀원들의 코드를 통합해서 전체적으로 테스트

테스트 전문가 테스트
  : 테스트 전문가가 테스트. 개발자가 하는 것 보다
  더 많은 버그. 수정사항 발견 가능

user테스트
  : 개발완료 후 사용자가 테스트