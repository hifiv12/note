## AOP라는 패러다임
  - 관점 지향 프로그래밍
    * 관심사의 분리
      + 핵심 로직이 아닌 전반적으로 반복 사용하며 필요한 로직들 
      + 횡단 관심사(cross-concerns)
  
  - 주요 용어
    * Aspect : 횡단 관심사 > 로깅, 보안, 트랜잭션 등
    * Advice : 횡단 관심사를 구현한 객체
    * Target : 핵심 로직을 가지고 있는 객체
    * Proxy 객체 : Target 객체 + Advice
    * JoinPoint
      + Advice의 적용 대상 - 스프링에서는 target의 메소드
    * PointCut  
      + 여러 JoinPoint들 중에서 Advice가 적용되는 select 기준

  - Advice의 종류
    * 실제로 개발하는 관심사 코드

    구분 | 설명
    -- | --
    Before Advice | Target의 JoinPoint를 호출하기 전에 실행되는 코드, 코드 실행 자체에 관여 불가
    After Returning Advice | 모든 실행이 정상적으로 이루어진 후 동작하는 코드
    After Throwing Advice | 예외가 발생한 뒤에 동작하는 코드
    After Advice | 정상적인 실행, 예외 발생시 실행, 둘의 구분없이 실행하는 코드
    Around Advice | 메서드의 실행 자체를 제어할 수 있는 가장 강력한 코드, 직접 대상 메서드를 호출, 결과나 예외를 처리

  - Pointcut
    * Advice를 어떤 JoinPoint에 결합할 것인지를 결정하는 설정

    구분 | 설명
    -- | --
    execution(@execution) | 메서드를 기준으로 Pointcut을 설정
    within(within) | 특정한 타입(클래스)을 기준으로 Pointcut 설정
    this | 주어진 인터페이스르 ㄹ구현한 객체를 대상으로 Pointcut 설정
    args(@args) | 특정한 파라미터를 가지는 대상들만 Pointcout 설정
    @annotaion | 특정한 어노테이션이 적용된 대상들만을 Pointcut으로 설정

  - AOP practice
    * pom.xml
      + org.aspectj-version : 1.9.0
      + org.slf4j-version : 1.7.25
      + dependencies
        - aspectweaver
    * root-context.xml
      + xmlns:aop="http://www.springframework.org/schema/aop"
      + <context:annotation-config></context:annotation-config>
      + <context:component-scan base-package="org.zerock.aop"><context:component-scan>
      + <aop:aspectj-autoproxy></aop:aspectj-autoproxy>	

  - @Around와 ProceedingJoinPoint
    * @Arround의 경우 직접 해당 메소드를 실행할 것을 결정할 수 있음
    * 파라미터로 ProceedingJoinPoint로 지정하고 사용해야함
    * ProceedingJoinPoint의 메서드
      + getTarget() : 실제로 실행해야 하는 객체
      + proceed() : 실제 메서드의 실행
    
## 스프링에서 트랜잭션 처리
  - 트랜잭션
    * 비즈니스 용어에서 '거래' 의 의미
    * 하나의 '거래'는 여러 번의 데이터베이스 관련 작업이 이루어지므로 이런 작업들을 '하나의 트랜잭션으로 처리'한다고 표현
    * 트랜잭션의 원칙 ACID
      + 원자성 : 하나의 트랜잭션은 모두 하나의 단위로 처리
      + 일관성 : 트랜잭션이 성공했다면 데이터베이스의 모든 데이터는 일관성을 유지해야만 한다.
      + 격리 : 트랜잭션으로 처리되는 중간에 외부에서의 간섭은 없어야만 한다.
      + 영속성 : 트랜잭션이 성공적으로 처리되면, 그 결과를 영속적으로 보관되어야 함

  - 댓글과 게시물의 반정규화
    * 정규화를 하면 여러번의 조인이 필요하고, 성능의 저하가 오는 경우 -> '반 정규화'를 통해서 해결
    * 반정규화는 자주 사용하는 값을 컬럼으로 작성해서 유지하는 방식
    * 게시물과 댓글의 숫자의 경우

  - 트랜잭션 설정의 테스트
    * 2개 이상의 테이블에 insert 작업을 하나의 '트랜잭션' 이라고 가정하고 트랜잭션 설정이 없는 경우와 있는 경우를 비교
    * 스프링의 경우 @Transactional을 이용해서 설정 가능
      + method @Transantional 의 설정이 가장 우선시
      + class @Transantional 설정은 메서드 보다 낮음
      + interface @Transactional 가장 낮은 우선순위

  - 댓글과 트랜잭션 설정
    * tbl_board 테이블 댓글 수를 replycnt 컬럼에 추가
    * 댓글의 추가와 삭제시에 replycnt는 트랜잭션 하에 관리

    ```sql
      alter table tbl_board add (replycnt number default 0);
      update tbl_board set replycnt = (select count(rno) from tbl_reply 
      where tbl_reply.bno = tbl_board.bno);
    ```

## 파일 업로드 방식
  - 일반적인 파일 업로드 처리 방식
    * form 태그를 이용하는 방식 -> 브라우저의 제한이 없어야 하는 경우
      + 일반적으로 페이지 이동과 동시에 첨부파일을 업로드 하는 방식
      + iframe 태그를 이용해 화면의 이동없이 첨부파일을 처리
    * ajax를 이용하는 방식 -> 첨부파일을 벼롣로 처리하는 방식
      + input 태그 속성 type='file'을 이용하고 Ajax로 처리하는 방식
      + Drag And Drop이나 JQuery 라이브러리들을 이용해서 처리

  - 파일 업로드 라이브러리
    * cos.jar > 비권장
    * commons-fileuploadd  > 일반적
    * 서블릿 3.0 이상 > 자체 API
  
  - 파일 업로드 전 설정
    * web.xml 
      + multipart-config
        - locaion
        - max-file-size
        - max- request-size
        - file-size-threshold
    * servlet-context.xml
      + context:component-scan > base-package = "org.zerock.controller"
      + beans:bean 
        - id > multipartResolver
        - class="org.springframework.web.multipart.support.StandardServletMultipartResolver"
  - form 방식
    * uploadForm.sjp 작성
    * Multipart 타입
      + 업로드 되는 파일 데이터 처리에 사용
      + 스프링의 컨트롤러의 파라미터로 처리

  - MultipartFile method
    + getName():String > 파라미터의 이름 input태그
    + getOriginalFileName():String > 업로드 되는 파일의 이름
    + isEmpty():boolean > 파일이 존재하지 않는 경우 true
    + getSize():long > 업로드 되는 파일의 크기
    + getBytes():byte[] > byte[]로 파일 데이터 변환
    + getInputStream() > 파일데이터와 연결된 InputStream을 반환
    + transferTo(File file) > 파일의 저장
    
  - Ajax를 이용한 파일 업로드
    * ajax를 이용하는 경우 FormData 객체를 이용
    * FormData 역시 브라우저 별로 지원 여부 확인

  - 파일 전송시 고려 사항들
    * 동일한 이름으로 파일 업로드 > 기존 파일 사라짐
    * 원본파일의 용량이 큰 이미지 파일 > 썸네일 생성해야됨
    * 이미지, 일반 파일과 구분하여 다운로드 혹은 페이지 조회하도록
    * 업로드 파일의 확장제 제한
    
## 파일 업로드 상세 처리
  - 파일 확장자와 크기 사전처리

  - 중복된 이름의 파일 처리
    * UUID 사용

  - 섬네일(thumbnail) 이미지 생성
    * 용량이 큰 원본 이미지 > 데이터 전송 문제
      + 작은 이미지(썸네일)을 생성해서 처리

  - 섬네일을 처리하는 단계
    * 이미지 파일 여부의 판단
    * 섬네일 생성 및 저장
