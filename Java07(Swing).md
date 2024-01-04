  - 바이트 스트림 클래스
    * 바이트 단위의 바이너리 값을 읽고 쓰는 스트림
    * InputStream / OutputStream
      + 추상 클래스 및 바이트 스트림 슈퍼클래스
    * FileInputStream / FileOutStream
      + 파일로부터 바이트 단위로 읽기/저장하는 클래스. 바이너리 파일 입출력 용도
    * DataInputStream / DataOutPutStream
      + 자바의 기본 데이터 타입의 값을 바이너리 값 그대로 입출력
      + 문자열도 바이너리 형태로 입출력
  
  - 버퍼 스트림 
    * 입출력 데이터를 일시적으로 저정하는 버퍼를 이용하여 입출력 효율 개선
    * 목적
      + 입출력 시 운영체제의 api 호출 횟수를 줄여 입출력 성능 개선
    * 종류
      + 바이트 버퍼 스트림 : 바이트 단위 바이너리 데이터
      + 문자 버퍼 스트림 : 유니코드 문자

  - File 클래스 (java.io.File)
    * 파일의 경로명을 다루는 클래스
    * 파일 관리 기능
      + 파일 이름 변경, 삭제, 디렉토리 생성, 크기 등 
      + File 객체는 파일 읽고 쓰기 기능 없음
    * 복사를 할때는 버퍼의 사용 유무에 따라 확연하게 속도차이가 있다.


9. 자바의 GUI 기초, AWT와 Swing
  - 자바의 GUI
    * 목적 
      + 그래픽 이용, 마우스 키보드의 입력 > 이해 쉬움
    * 특징
      + 쉬운 gui 컴포넌트, 프로그래밍
    * 방법
      + AWT 
      + Swing

  - AWT와 Swing 패키지
    * AWT (Abstract Windowing Toolkit)
      + 운영체제의 gui 컴포넌트의 도움을 받아 작동 > 처리 속도 빠름 
    * Swing (스윙)
      + 순수 자바 언어로 만들어진 라이브러리
      + 경량 컴포넌트 > 운영체제에 의존하지 않음

  - Swing
    * 스윙 컴포넌트 2가지
      + JCOmponent
      + AWT의 Container를 상속 받는 클래스
    * JCOmponent
      + 스윙 컴포넌트의 공통 속성을 구현한 추상 클래스
      + AWT의 Component를 상속받음

  - Container and Component
    * 컨테이너 (java.awt.Container)
      + 다른 GUI 컴포넌트를 포함할 수 있는 컴포넌트
      + 다른 컨테이너에 포함 될 수 있음
    * 최상위 컨테이너
      + 다른 컨테이너에 속하지 않고 독립적으로 화면에 출력 가능한 컨테이너
      + 모든 컴포넌트는 컨테이너에 포함되어야 화면에 출력 가능
    * 컴포넌트
      + 컨테이너에 포함되어야 하면에 출력될 수 있는 순수 컴포넌트
      + 모든 컴포넌트는 java.awt.Component를 상속
      + 모든 스윙 컴포넌트는 javax.swing.JComponnent를 상속받음

  - 스윙 프레임
    * 모든 스윙 컴포넌트를 담는 최상위 gui 컨테이너
      + JFrame 상속
      + 컴포넌트가 화면에 보이려면 스윙 프레임 내에 부착
      + 프레임을 닫으면 모든 컴포넌트가 안보임
    * 스윙 프레임 기본 구성
      + 프레임 - 스윙 프로그램의 기본 틀
      + 메뉴바 - 메뉴들이 부착되는 공간
      + 컨텐트 팬 - GUI 컴포넌트들이 부착되는 공간

  - 스윙 응용프로그램의종료
    * frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      + 프레임 종료 버튼시 응용프로그램이 종료되도록

  - main() 종료 뒤에도 프레임이 살아 있는 이유?
    * 메인 스레드
    * 이벤트 분배 스레드
    * 실행 중인 사용자 스레드가 하나도 없을 때 종료
    * 메인이 종료되어도 이벤트 분배 스레드가 살아 있어 화면에 보임

  - 컨테이너와 배치관리자
    * 컨테이너의 디폴트 배치관리자
      + 생성시 디폴트 배치관리자 설정
    * 새로운 배치관리자 설정
      + Container.setLayout(LayoutManager lm)
    
  - FlowLayout
    * 배치방법
      + 컨테이너 공간 내에 왼쪽에서 오른쪽으로 배치 / 위에서 아래로
      + 크기 변하면 컴포넌트 재배치
    * 생성자와 속성
      + 생성자 : FlouwtLayout(int align, int hGap, int vGap)
      + 속성
        - align
        - hGap : 좌우 컴포넌트 수평 간격 default 5
        - vGap : 상하 컴포넌트 수직 간격 default 5

  - borderLayout
    * 배치방법
      + 5구역으로 분할 및 배치
        - east, west, sourth, north, center
      + add(Component comp, int index)
      + 크기가 변하면 재배치
    * 생성자와 멤버함수
      + 생성자
        - BorderLayout(int hGap, int vGap)
      + add() 멤버 함수
        - BorderLayout.EAST or WEST or SOUTH or NORTH or CENTER

  - GridLayout
    * 배치방법
      + 컨테이너 공간을 동일한 사각형 격자로 분할하고 각 셀 마다 컴포넌트 배치
      + 생성자에 행수와 열수를 지정
      + 왼 -> 오 , 위 -> 아래
      + 컨테이너의 크기가 변하면 재배치
    * 생성자
      + GridLayout(int rows, int cols, int hGap, int vGap)

  - 배치관리자 없는 컨테이너
    * 응용 프로그램에서 컴포넌트의 절대 크기와 절대 위치 결정
    * 개발자의 임의로 결정하고자 하는 경우
    * 컴포넌트의 위치와 크기가 수시로 변하거나, 겹치게 출력할경우
    * 배치관리자 제거방법
      + container.setLayout(null);
    * 컴포넌트의 절대 크기와 절대 위치 설정
      + 크기설정 : .setSize(int width, int height);
      + 위치설정 : .setLocation(int x, int y);
      + 동시설정 : .setBounds(int x, int y, int width, int height);


10. 자바의 이벤트 처리
  - 이벤트 기반 프로그래밍
    * 이벤트 종류
      + 사용자의 입력 : 키보드 마우스 등등
      + 센서의 입력, 데이터 송수신
      + 응용프로그램, 스레드의 메세지
    * 구조
      + 이벤트 리스너 들의 집합
    * 처리 순서
      + 이벤트 발생 > 객체 생성 > 찾기 > 호출 > 실행

  - 이벤트 관련 용어
    * 이벤트 소스
      + 이벤트를 발생시킨 gui 컴포넌트
    * 이벤트 객체
      + 발생한 이벤트에 대한 정보
    * 이벤트 리스너
      + 이벤트를 처리하는 코드
      + 컴포넌트에 등록되어야 작동가능
    * 이벤트 분배 스레드
      + jvm으로부터 이벤트 발생 통지
      + 이벤트 소스와 이벤트 종류 결정
      + 적절한 이벤트 객체 생성 및 리스터를 찾아 호출

  - 이벤트 객체
    * 이벤트가 발생할 때, 발생한 이벤트에 관한 정보를 가진 객체
    * 이벤트 리스너에게 전달됨

  - 이벤트 객체에 포함된 정보
    * 정보
      + 이벤트 종류
      + 이벤트 소스
      + 이벤트가 발생한 화면 좌표
      + 이벤트가 발생한 컴포넌트 좌표
      + 버튼이나 메뉴 아이템의 문자열
      + 클릭된 마우스 버튼 번호
      + 클릭 횟수
      + 키의 코드 값과 문자 값
      + 체크 상태
    * 이벤트에 따른 정보 포함
      + actionEvent : 액션 문자열
      + MouseEvent : 마우스의 위치 정보, 버튼, 함께 누럴진 키 등등
      + ItemEvent : 아이템의 체크 상태

  - 이벤트 리스너
    * 이벤트를 처리하는 코드, 클래스로 작성
    * 이벤트 리스너 작성을 위한 인터페이스 제공
    * 컴포넌트는 다른 이벤트에 대한 리스터를 동시에 여러개 가질 수 있음

  - 이벤트 리스너 작성 방법
    * 독립 클래스로 작성 > 여러곳 사용
    * 내부 클래스로 작성 > 특정 클래스에서만 사용
    * 익명 클래스로 작성 > 간단한 경우
    
  - 익명 클래스
    * 클래스 정의 + 인스턴스 생성을 한번에 작성
    * ActionListener를 구현하는 익명의 이벤트 리스너 작성


--------------------------------------------------------------------



버퍼
  원래는 cpu와 보조기억장치 혹은 메모리의 처리속도 차이 때문에 고안
  버퍼에 데이터를 쌓은 다음 cpu가 한꺼번에 처리
  버퍼에 데이터가 쌓일 동안 cpu는 다른 작업을 할 수 있다.

CLI (Command Line Interface)
  : 명령어 기반 인터페이스
  -> text 위주

GUI (Graphic User interface)
  : 그래픽 유저 인터페이스
  -> window 기반

window 프로그램은 이벤트 기반 개발
  -> 

JavaFx

Component
  : 부품

button, radiobutton 등을 component라고 함
 
MS-Windows

visual c++ -MFC
  : 배우기 어렵다. 구현하기 어렵다. 속도 빠르다
Visual Basic
  : 배우기 쉽다. 구현하기 쉽다. 속도 느리다

ASP
  : vB 기반 
  -> 동시접속자가 많고 처리량이 많은 서버구축시 성능 부족

JSP
  : 자바기반
  -> ASP 보다 성능 우수

C#
  : 자바를 벤치마킹해서 만듦
  -> JVM vs .NET FrameWork

VB.net
  : visual Basic의 oop화

ASP.NET
  : C# 기반 or VB.NET기반

----------------------------
국내에서 window프로그래밍

근래에는 visual c#

java는 웹

----------------------------

Event
  : 