  - 어댑터(Adapter) 클래스
    * 리스너의 모든 메소드가 단순 리턴하도록 구현해 놓은 클래스

  - key 이벤트와 포커스
    * 키 입력시 key 이벤트 발생
      + 키를 누를 때
      + 누른키를 떼는 순간
      + 누른 키를 떼는순간(uincode)
    * 현재 포커스를 가진 컴포넌트
    * focus
      + 컴포넌트나 응용프로그램이 키 이벤트를 독점하는 권한
      + 컴포넌트에 포커스 설정 방법

        ```java
          component.setFocusable(true); // component가 포커스를 받을 수 있도록 설정
          component.requestFocus(); // componen에 포커스 강제 지정
        ```

    - 컴포넌트에 포커스 주기
      * 스윙 프레임이 만들어질 포커스를 지정
        + JFrame setVisible(true) 이후 포
        커스
      * 마우스로 컴포넌트를 클릭할 때 포커스 지정
        + 언제든지

    - KeyListener의 메소드와 키
      * 3개의 메소드
        + KeyPressed
        + KeyReleased
        + KeyTyped
      * 컴포넌트 키 이벤트 리스너 등록

    - 키 2종류
      * 유니코드 키
        + 호출 순서 : KeyPressed(), keyTyped(), KeyReleased()
      * 유니코드가 아닌 키
        + 문자 키가 아닌 제어키 : fn, home, up, delete, control, shift, alt ..etc -> 가상 키 코드값이 존재
        + 호출 순서 : KeyPressed(), KeyReleased()
      * 가상 키 
        + 가상 키 코드는 KeyEvent 클래스에 상수로 선언

    - 입력된 키 판별 (KeyEvent 객체)
      * 키의 유니코드 알아내기 KeyEvent.getKeyChar()
      * 입력된 키의 가상 키 값 알아내기 KeyEvent.getKeyCode()
      * 키 이름 문자열 리턴 KeyEvent.getKeyText(int KeyCode)
        + Static 메소드

  - 마우스 이벤트와 마우스 관련 리스너
    * MouseListener
      + mouseEntered
      + mouseExited
      + mousePressed
      + mouseReleased
      + mouseClicked
    * MouseMotionListener
      + mouseDragged
      + mouseMoved
    * MouseWheelListener
      + mouseWheelMoved

  - MouseEvent 객체의 정보 (MouseEvent e)
    * 마우스 포인터의 위치 e.getX or Y
    * 입력된 마우스 버튼 e.getButton()
    * 마우스 클릭 횟수 e.getClickCount()

11. 기본적인 스윙 컴포넌트와 활용
  - 컴포넌트 기반 gui 프로그래밍
    * 구성 쉬움
    * 컴포넌트 한계
    * 일반적인 gui 한계

  - 그래픽 기반 gui 프로그래밍
    * 직접 그려내는 그래픽 화면 구성 
    * 작업 부담 높음 
    * 자유로운 gui
    
  - JLabel, 레이블 컴포넌트
    * 문자열이나 이미지를 컴포넌트화 하여 출력하기 위한 목적
    * 생성자
      + 인자
        - ()
        - img 
          * ImageIcon 클래스 사용
          * png, gif, jpg 확장자 사용
        - String
          * 단순 텍스트
        - 속성
      + 인자를 모두 사용해 생성할 수 있다.

  - JButton, 버튼 컴포넌트
    * 버튼 모양의 컴포넌트, 선택하면 Action 이벤트 발생
    * 생성자
      + 인자
        - ()
        - 이미지
        - 문자열
        - 문자열과 이미지 
    * 이미지 버튼 만들기
      + 마우스 접근에 따른 서로 다른 이미지 출력가능

  - 레이블과 버튼 정렬
    * 수평정렬
    * 수직정렬

  - JCheckBox, 체크박스 컴포넌트
    * 선택과 비선택의 두 상태만 가지는 체크 버튼
    * 생성자
      + 인자
        - ()
        - 문자열
        - 이미지
        - 문자열과 이미지
        - boolean
    * item 이벤트 처리
      + 체크 박스나 라디오버튼 선택 상태가 바뀐것이 발생하는 이벤트
      + 인터페이스 추상 메소드
        - void itemStateChanged(ItemEvent e)
      + ItemEvent의 주요 메소드
        - getStateChange()
        - getItem()

  - JRadioButton, 라디오버튼 컴포넌트
    * 여러 버튼으로 그룹 형성, 하나만 선택
    * 생성 과정
      + 버튼 그룹 객체 생성
      + 라디오 버튼 컴포넌트 생성
      + 라디오 버튼을 버튼 그룹에 삽입
      + 라디오 버튼을 컨테이너에 삽입

  - JTextField, 텍스트필드 컴포넌트
    * 텍스트 입력창
    * <Enter> 입력되면 Action 이벤트 발생
    * 주요 메소드
      + .setEditable(false);
      + .seText("test");
      + setFont(new Font("고딕체", Font.ITALIC, 20));

  - JTextArea, 텍스트 영역 컴포넌트
    * 여러줄 입력가능한 텍스트 입력창
    * JScrollPane 컴포넌트 삽입 시 스크롤바 지원

--------------------------------------------

Event 처리를 Adaptor를 사용할 경우 Adaptor Class이므로 더이상 다른 클래스를 상속 받을 수 없다.
Adapter대신 Listener를 상속 받으면  Listener는 interface이므로 다른 클래스를 상속받을 수 잇다.

엔터키도 액션리스터이다.
