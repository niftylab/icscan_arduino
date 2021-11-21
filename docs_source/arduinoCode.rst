dataTransfer.ino
===================

overview
--------------------
#. 시리얼 통신을 통해 비트스트림을 컴퓨터로부터 받아오고 그 스트림을 칩에 보낸다.
#. 실행 환경: 아두이노 우노, SPI.h 모듈 필요(웬만해선 아두이노 ide 설치할 때 기본으로 깔려있음)
#. 프로그램 실행순서
 
    :step1: 변수, 핀, 통신 초기화
    :step2: 컴퓨터에서 시리얼 통신으로 데이터가 올 때 까지 대기
    :step3: 받은 값 컴퓨터에 재전송(재대로 받았는 지 확인하기 위해서)
    :step4: 받아온 비트스트림을 SPI통신을 통해 칩으로 전송
    :step5: 컴퓨터에 SPI통신이 끝났음을 알림
    :step6: step2로 돌아감
   
CLK, DATA, EN, RST핀
-------------------------
#. CLK: 13번핀, DATA: 11번핀, EN: 10번핀, RST: 9번핀
#. 초기 상태  -> CLK : IDLE,  DATA: X,  EN: LOW,  RST: LOW
#. SPI 통신단계

    :step1: 통신시작 전 RST핀에서 펄스 출력
    :step2: EN핀을 HIGH로 올리고 데이터 전송 시작
    :step3: 데이터 전송 후 EN핀을 LOW로 내리고 통신 끝
  
수정해줘야 하는 변수
----------------------

#. _MAXBYTES: 
    * 한번에 보내고 싶은 최대 바이트 수
    * 최대 255까지 가능( 더 늘리고 싶다면 코드를 수정해야 함)
        
#. SPI_MODE: 
    * clk의 idle 값, falling/rising edge transfer 를 정할 수 있다. 
    * SPI_MODE0: CLK idle = low, bit transfer = rising edge
    * SPI_MODE1: CLK idle = low, bit transfer = falling edge
    * SPI_MODE2: CLK idle = HIGH, bit transfer = falling edge
    * SPI_MODE3: CLK idle = HIGH, bit transfer = rising edge
        
#. MSBFIRST/LSBFIRST: 
    * most/least significant bit first