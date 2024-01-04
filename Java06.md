  - 주요 패키지
    * java.lang > 자동으로 import, 나머지 아래의 패키지는 import 명시
    * java.util
    * java.io
    * java.awt
    * javax.swing

  - Object 클래스 
    * 모든 클래스의 수퍼 클래스
    * 모든 객체가 공통으로 가지는 객체의 속성을 나타내는 메소드 보유

    메소드 | 설명
    -- | --
    boolean equals(object obj) | ojb가 가리키는 객체와 현재 겍체를 비교하여 같으면 true 리턴
    Class getClass() | 현 객체의 런타임 클래스를 리턴
    int hashCode() | 현 객체에 대한 해시 코드 값 리턴
    String toString() | 현 객체에 대한 문자열 표현을 리턴
    void notify() | 현 객체에 대해 대기하고 있는 하나의 스레드를 깨운다.
    void notifyAll() | 현 객체에 대해 대기하고 있는 모든 스레드를 깨운다.
    void wait() | 다른 스레드가 깨울 때까지 현재 스레드를 대기하게 한다.

  - 객체 비교
    *  == : 레퍼런스를 비교
    * .equals() : 객체 내용을 비교

  - Wraaper 클래스
    * 기본 8 개 타입을 클래스화한 클래스 > 객체로 다룰 수 있게 해줌

  - 박싱과 언박싱
    * 박싱(boxing) 기본 타입의 값을 Wrapper 객체로 변환
    * 언박싱(unboxing) Wrapper 객체에 들어 있는 기본 타입의 값을 빼내는 것
    * 자동 박싱과 자동 언박싱이 됨 

  - String의 특징
    * String - java.lang.String
    * 스트링 객체는 수정 불가능 -> 
    * 하나의 문자열 표현
    * 비교는 equals()
    * 주요 메소드
      - charAt(inx index)
      - compareTo(String anotherString)
      - length()
      - toLowerCase()
      - toUpperCase()
      - trim()

  - StringBuffer 클래스
    * 가변 크기의 문자열 저장 클래스
    * 인덱스 번호에 맞게 문자 하나씩 저장
    * 인덱스로 접근 하여 특정 인덱스 수정 가능
    * 주요 메소드
      - capacity() : 현재 크기 리턴
      - delete(int n, int m) : n~m의 인덱스 사이의 값을 삭제
      - insert(int n , String str) : n의 인덱스를 기준으로 문자 삽입

  - StringTokenizer 클래스
    * 하나의 문자열을 여러 문자열 분리
      - 구분 문자를 입력 > new StringTokenizer(str, "&");
      - String 클래시의 split()을 이용하여 동일 구현 가능 

  - Math 클래스
    * 산술 연산 메소드 제공 
    * 모든메소드는 static 타입 > 클래스 이름으로 바로 호출
    * 활용
      - 난수 : Math.random()*100+1 // 1~100 사이 랜덤 정수

  - Calendar 클래스
    * 시간, 날짜 정보 저장관리
    
    필드 | 의미 
    -- | --
    YEAR | 년도
    MONTH | 달(0~11)
    HOUR | 시간(0~11)
    HOUR_OF_DAY | 24시간 기준 시간
    SECOND | 초
    DAY_OF_MONTH | 한 달의 날짜
    DAY_OF_WEEK | 한 주의 요일
    AM_PM | 오전인지 오후인지 구분
    MINUTE | 분
    MILLISECOND | 밀리초


7. 제네릭과 컬렉션
  - Collection의 개념
    * 요소 객체들의 저장소 = 컨테이너
    * 요소의 개수에 따라 크기 자동조절 > 고정 크기의 배열을 다루는 어려움 해소
    * 삽입, 삭제에 따른 요소의 위치 자동 이동 > 다양한 객체 관리 용이
  
  - 컬렉션과 제네릭
    * 컬렉션
      - 제너릭 기법으로 구현
      - 컬렉션의 요소는 객체만 가능 > 기본타입 사용시 자동 변환(객체로)
    * 제네릭
      - 특정 타입만  다루지 않고, 여러 종류의 타입으로 지정할수 있도록 클래스나 메소드를 일반화 시키는 기법
      - <E>, <K>, <V> : 타입 매개 변수
  
  - Vector<E>
    * 여러 객체들을 삽입, 삭제, 검색하는 컨테이너 클래스
    * Vector에 삽입 가능한 것
      * 객체, null, Warraper 객체
    * 삽입 
      - 맨 뒤, 또는 중간
    * 삭제
      - 원하는 위치의 객체 삭제 > 자동 자리 이동
    * 메소드
      - add(n, m) : n -> index, m -> value
      - size() : length
      - capacuty()
      - get(n) : n -> index
      - remove(n) : n -> index
      - lastElement()
      - removeAllElement()





---------------------------------------------------------------------




== 
  : 값이 같은지를 비교
  => 비교대상이 reference 변수 일 때 reference 변수에 저장된 reference 값이 같은지 비교

equals()
  : reference 변수 값이 가리키는 데이터가 같은지 비교
  => Object 클래스 비교는 instanceOf

StringBuffer의 메소드들은 원본을 사용
  원본이 바뀌어도 될 경우에는 StringBuffer를 사용하는 것이 메모리 절약
  일반적으로는 String을 사용하나 튜닝할 때 StringBuffer 사용 고려

StringBuilder도 원본 사용

-----------------------------------------------------------------------------------

간결한게 좋다
Simple is Best

이해하기 쉬운 코드가 좋다
어려운 것도 쉽게 코딩

함수는 
  1.같은 코드를 응용프로그램 여러곳에서 반복사용 
  2.같은 코드를 다음 프로젝트에서 또 많이 사용할 경우
  3.특정 기능 코드를 정리할 경우