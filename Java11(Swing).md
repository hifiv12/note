  - 다이얼로그
    * 사용자로부터 입력 받기 위한 대화 상자
    * JDialog
      + 최상위 컨테이너 -> 다른 컨테이너에 속할 필요 없이 화면 출력가능
    * 모달 다이얼로그
      + 사용자 입력을 독점하는 다이얼로그, 닫기전까지 다른 창에서 작업을 전혀 할 수 없는 다이얼로그
      + JDialog(Frame owner, String title, boolean modal) 생성자에 modal을 true
    * 모달리스 다이얼로그
    * 팝업 다이얼로그, JOptionPane
      + JOptionPane
        - 팝업 다이얼로그 지원
      + 입력 다이얼로그
        - 한 줄을 입력 받는 다이얼로그
      + 확인 다이얼로그
        - 사용자로부터 Yes/No 등 확인을 입력받는 다이얼로그
      + 메세지 다이얼로그
        - 단순 메세지를 출력하는 다이얼로그
    * 파일 다이얼로그
      + JFileChooser
        - 파일 시스템의 탐색기와 같은 기능을 하는 다이얼로그
        - 사용자에게 파일이나 디렉터리를 쉽게 선택하도록 하는 기능
        - 종류
          + 파일 열기 다이얼로그 (File Open Dialog)
          + 파일 저장 다이얼로그 (File Save Dialog)
    * 컬러 다이얼로그
      + JColorChooser
        - 색상 팔레트를 제공하는 모달 다이얼로그

  - 탭팬
    * 여러 패널을 겹치게 하여 공간을 공유토록 지원하는 팬
    * 메소드
      + addTab(String title, Componenet comp)
      + getTabpCount()
      + getSelectedIndex()
      + getSelectedComponent()
      + remove()
      + setTabPlacement(int tabPlacement)
    
  - 오디오 관련

15. 네트워크
  - OSI 7 계층
    * 계층이 낮을 수록 h/w와 관련, 높을수록 app과 관련
      + 1계층 : 물리
      + 2계층 : 데이터링크
      + 3계층 : 네트워크
      + 4계층 : 전송
      + 5계층 : 세션
      + 6계층 : 표현
      + 7계층 : 응용
    * 네트워크 및 전송 계층: TCP/IP
    * TCP/IP 프로토콜
      + Transmission Control Protocol
      + 두 시스템 간 신뢰성 있는 데이터의 전송을 관장하는 프로토콜
      + TCP에서 동작하는 응용 프로그램
        - email
        - ftp
        - http
    * IP
      + Internet Protocol
      + 패킷 교환 네트워크에서 송신 호스트와 수신 호스트가 데이터를 주고 받는 것을 관장하는 프로토콜
    
  - IP 주소
    * 네트워크 상에서 유일하게 식별될 수 있는 컴퓨터 주소
    * 문자열로 구성된 도메인 이름으로 바꿔 사용(DNS)
    * 현재 32비트 IPv4 -> IPv6로 점점 늘어가는중
    * IP 주소 확인 cmd ipconfig

  - 포트
    * 포트번호를 통해 통신할 응용프로그램 식별
    * 모든 앱은 하나 이상의 포트 생성 가능
    * well-known-ports
      + 시스템이 사용하는 포트 0~1023사이
  
  - 소켓 프로그래밍
    * 소켓: tcp/ip 네트워크를 이용해 통신 프로그램을 작성하도록 지원하는 기술
      + 소켈끼리 데이터 주고 받음
      + 특정 IP포트 번호와 결합
    + 서버 소켓과 클라이언트 소켓

  - socket 클래스, 클라이언트 소켓
    
    생성자 | 설명
    -- | --
    Socket | 연결되지 않은 상태의 소켓을 생성
    Socket(InetAddress, int port) | 소켓을 생성하고, 지정된 ip주소와 포트번호에서 대기하는 원격 응용프로그램의 소켓에 연결
    Socket(String host, int port) | 소켓을 생성하여 지정된 호스트와 포트 번호에 연결한다. 호스트 이름이 null인 경우 루프백 주소로 가정

  - Socket 클래스의 메소드

    메소드 | 설명
    -- | --
    void bind(SocketAddress bindpoint) | 소켓에 로컬 ip주소와 로컬포트를 지정 
    void close() |소켓 닫기
    void connect(SoketAddress endpoint) | 소켓을 서버에 연결
    InetAddress getInetAddress() | 소켓에 연결된 서버 ip주소 변환
    InputStream getinputStream() | 소켓에 연결된 입력 스트림 반환, 이 스트림을 이용해 소켓에 연결된 상대방으로부터 받은 데이터를 읽을 수 있음
    Inetaddress getLocaladdress() | 소켓이 연결된 로컬주소 반환
    int getLocalPort() | 로컬포트 번호 반환
    int getPort() | 연결된 서버 포트 번호 반환
    OutputStream getOutputStream() | 연결된 출력 스트림 반환
    boolean isBound() | 로컬주소에 연결되어있다면 true
    boolean isCnnecteded | 서버 연결 true
    boolean isClosed() | 닫혀있으면 true
    voide setSoTimeout(int timeout)



  -----------------------------------------------------------------

Protocol
  : 통신규약
  -> 쌍방간에 통신을 하기 위한 규칙

HTTP(Hyper Text Transfer Protocol)
