2. 자바 기본 프로그래밍
  - 클래스와 메소드
  - 식별자
    * 클래스, 변수, 상수, 메소드 등에 붙이는 이름
    * _, $를 제외한 특수문자, 공백 또는 탭은 사용 불가
    * 대소문자 구분
  - 자바 키워드
  - 좋은 이름 붙이는 언어 관습
    * 가독성 높은 이름
    * 헝가리언 이름 붙이기
    * camelcase
    * 상수는 모든 문자를 대문자
  - 자바의 데이터 타입
    * 기본 타입
      - boolean : 1비트, true or false
      - char : 2바이트, unicode
      - byte : 1바이트 -128 ~ 127
      - short : 2바이트, -32768 ~ 32767
      - int : 4바이트 -2^31 ~ 2^31-1
      - long : 8바이트 -2^63 ~ 2^63-1
      - float : 바이트 -3.4E38 ~ 3.4E38
      - double : 바이트 -1.7E308 ~ 1.7E308
    * 레퍼런스 타입 
      - 배열
      - 클래스
      - 인터페이스
  - 문자열
    * 문자열은 기본 타입이 아님
    * String 클래스로 문자열 표현
  - 변수와 선언
    * 변수
      - 프로그램 실행 중에 값을 임시 저장하기 위한 공간
      - 데이터 타입에서 정한 크기의 메모리 할당
  - 리터럴과 정수 리터럴
    * 리터럴
      - 프로그램에서 직접 표현한 값
      - 정수, 실수, 문자, 논리, 문자 리터럴
    * 정수 리터럴
      - 10/8/16/2진수 리터럴
      - 정수 리터럴은 int형으로 컴파일
      - long타입은 숫자뒤에 L을 표시
  - 실수 리터럴
    * 소수점 형태나 지수 형태로 표현한 실수
    * double 타입으로 컴파일
  - 문자 리터럴
    * ''로 문자 표현
    * \u 다음에 유니코드
    * 특수문자 리터럴

      종류 | 의미
      -- | --
      '\b' | backspace
      '\t' | tap
      '\n' | line feed
      '\f' | form ffed
      '\r' | carriage return
      '\"' | double quote
      '\'' | single quote
      '\\' | backslash

  - 논리 리터럴과 boolean 타입
    * 논리 리터럴 -> true or false
  - 이외의 리터럴
    * null 리터럴
    * String 리터럴
      - double quote로 묶어 표현
      - 문자열 리터럴은 String 객체로 자동 처리
  - var 키워드
    * auto 키워드 > 컴파일러가 변수 타입 추론
    * 지역 번수 선언에만 사용
    * 변수 선언문에 반드시 초기값 지정
  - 상수
    * 상수선언
      - final 키워드
      - 선언 시 초기값 지정
      - 실행 중 값 변경 불가
  - 자동 타입 변환
    * 작은 타입은 큰 타입으로 자동 변환
    * 치환문(=)이나 수식 내에서 타입이 일치하지 않을 때
  - 강제 타입 변환
    * 큰 타입이 작은 타입으로 변환 > 자동 변환 안됨
    * 필요에 의해 강제로 타입 변환을 지시
      - 강제 변환 시 값 손실 우려
  - Scanner로 쉽게 키 입력
    * Scanner 클래스
    * import java.util.Scanner
    * Scanner sc = new Scanner(System.in) 객체 생성
    * 메소드
      
      메소드 | 설명
      -- | --
      String next() | 다음 토큰을 문자열로 리턴
      byte nextByte() | 다음 토큰을 byte로 리턴
      short nextShort() | 다음 토큰을 short로 리턴
      int nextInt() | 다음 토큰을 int로 리턴
      long nextLong() | 다음 토큰을 long로 리턴
      float nextLong() | 다음 토큰을 float로 리턴
      double nextDouble() | 다음 토큰을 double로 리턴
      boolean nextBoolean()| 다음 토큰을 boolean로 리턴
      String nextLine() | '\n'을 포함하는 한 라인을 읽고 '\n'을 버린 나머지 문자열 리턴
      void close() |  Scanner close
      boolean hasNext() | 입력된 토큰이 있으면 true or 입력 때까지 무한정 대기 and ctrl+z키 입력되면 false 리턴

  - 식과 연산자
    * 연산 : 주어진 식을 계산하여 결과를 얻어내는 과정
    * 연산자 우선순위 
      - 괄호 > (부정/증감) > (곱셈/나눗셈) > (덧셈/뺼셈) > (비트 쉬프트) > (관계) > 비트 논리연산 > 논리곱 > 논리합 > 조건 > (대입/할당)
  - 산술 연산자
    * \+ \- \* \/ \%
  - 증감 연산
    * 1 증가 혹은 감소 시키는 연산

    연산자 | 내용
    -- | --
    a++ | a를 1 증가하고 증가 전의 값 반환
    a-- | a를 1 감소하고 감소 전의 값 반환
    ++a | a를 1 증가하고 증가된 값 반환
    --a | a를 1 감소하고 감소된 값 반환

  - 대입 연산
    * 연산의 오른쪽 결과는 왼쪽 변수에 대입
  - 비교 연산과 논리 연산
    * 비교 연산
      - 비교 연산자를 사용해 두항을 비교하여 참이면 true, 거짓이면 false를 리턴
    * 논리 연산
      - AND(&&), OR(||), NOT(!), XOR(^)을 사용해 두항을 논리연산 하여 참 -> true, 거짓 -> false
  
  - 조건 연산자 ? :
    * condition ? opr2 : opr3
      - condition 이 true -> opr2, false -> opr3
    * 간결하게 표현됨
  
  - 비트 연산
    * 1byte = 8bit
    * 비트 연산
      - 비트 논리 연산
        * AND(&), OR(|), XOR(^), NOT(~)
      - 비트 시프트 연산
        * > 일 경우 최상위부터 0으로 채움
        * < 일 경우 최하위부터 0으로 채움
  
  - 단순 if문
    * if의 괄호 안에 조건식
  - if - else
    * 조건식이 true면 실행문장1을 false면 실행문장2
  - 다중 if - else
    * if-else 가 연속되는 모양
  - switch문
    * case의 비교 값과 일치하면 해당 case의 실행문장 수행
    * 모든 값과 일치 하지 않으면 default 문 실행
    * default문 생략 가능
    * break문을 만나면 switch문 탈출 
    * case문의 값 -> 문자, 정수, 문자열 리터럴만 허용

3. 반복문과 배열 그리고 예외 처리
  - 반복문의 특징
    * for
    * while
    * do while
  - for문의 구성
    * for (초기문; 조건식; 반복 후 작업) { ..작업문.. }
  - while (조건식) { ..작업문.. } 
    * 반복 조건이 true면 반복, false면 종료
    * 처음부터 반복 조건을 통과한 후 작업문 수행
  - do { ..작업문.. } while(조건식);
    * 무조건 최소 한번 작업문 실행
  - 중첩 반복
    * 반복문 안에 반복문을 내포하는 구조
  - continue문
    * 반복문을 빠져 나가지 않으면서 다음 반복으로 진행
  - break문
    * 반복만 하나를 완전히 빠져 나갈 때 사용
  






-------------------------------------------------------------------
문자열 
  : 문자(character)의 배열
  c에서는 char[] 배열 사용
  java에서는 String 클래스 사용

메모리할당 (memory Allocate)

reference
  : instance를 가리키는 값
  -> c언어의 pointer와 비슷한 역할
  pointer는 직접 access
  reference는 간접 access

null은 reference 값이 없다는 의미

정수/정수 => 정수
  : 분모가 분자보드 크면 0이 된다.

백분율 구할 때 주의
  :(1월매출/1년매출)*100 => X
  -> (1월매출*100)/1년메출 => O

표준입출력
  표준입력 - 키보드
  표준출력 - 모니터

  그외의 입력 장치 - 마우스, 스캐너, 바코드스캐너
  그외의 출력 장치 - 프린터

비트 연산자가 사용되는 분야
  1.hardware_control
  2.image_processing
