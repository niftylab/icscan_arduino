setup
======

파이썬 모듈 설치 방법 (윈도우 기준)
------------------------------------

:step1: cmd를 관리자 권한으로 실행

:step2: pip install PyYAML 입력

:step3: pip install PySerial 입력
    
설치가 안될 시
--------------

:step1: pip PATH가 설정돼있는지 확인

* Python3: 
    * C:\\Users\\UserName\\AppData\\Local\\Programs\\Python\\Python38\\Scripts
    * 보통 Python\\Python38\\Script 에 저장되어 있음

* Anaconda3: 
    * c:\\ProgramData\\Anaconda3\\Scripts 
    * 단 필자는 아나콘다로 실행해본 적은 없음

:step2: pip가 설치돼있는지 확인

.. note::
    'venv\Lib' 이런 경로에 있는 파일이 아니라 위 경로와 비슷한 경로에 설치돼있어야 한다.
    만약 안돼있다면 `링크`_ 참조
            
.. _링크: https://dora-guide.com/pip-install/
     
:step3: 설치 후, **step1** 다시 시도

시리얼 포트 설정
----------------

:step1: 아두이노와 컴퓨터 usb연결

:step2: 장치 관리자 -> 포트 -> Arduino Uno(COMx) -> 포트 설정

:step3: 설정 내용 -> 비트/초: 115200, 데이터 비트: 8, 패리티: 없음, 정지 비트: 1, 흐름 제어: 없음