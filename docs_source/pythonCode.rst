makeStream.py
==============

overview
------------

* 같은 폴더에 있는 'test.yml'파일을 읽고 비트스트림을 만들어 시리얼 통신을 통해 아두이노로 보낸다.
* 비트스트림은 MSB first 기준으로 만든다.

실행환경
---------

* 윈도우, python3, PyYAML모듈, PySerial모듈이 필요하다.
* idle: 기본 python idle가능, vscode는 Python, Python for VSCode extension이 설치되어 있는 상황에서 실행함.

프로그램 실행 단계
----------------

:step1: test.yml 파일 읽어오기

.. code-block:: python

    with open('test.yml') as bit:
    stream = yaml.load(bit,Loader=yaml.FullLoader)

:step2: 시리얼 통신 연결 및 초기화
    
Serial( 'COMx', 115200 ) 에서 'COMx'값은 setup페이지에서 "시리얼 포트 설정" 항목 참조에서 확인하고 같은 값으로 바꿔준다.

.. code-block:: python

    ser = serial.Serial('COM4', 115200)
    if ser.readable():
       ser.read() # to clear buffer

:step3: test.yml 에서 읽어온 데이터로 비트스트림 생성 및 아두이노로 송신

.. code-block:: python

    for seg in stream[key].values():
        for i in range(0,8):
            bitStream[idx] = bitStream[idx] | (seg[i] << (7-i) )
        idx = idx + 1
    ...
    ser.write(bitStream)

:step4: 올바른 데이터를 보냈는지 체크

.. code-block:: python

    compare = True
    for i in range(0, datalen):
        if bitStream[ i+1 ] != receive[ i ]:
            compare = False
    #if compare == true -> correct data

:step5: 아두이노에서 칩으로 데이터를 보냈는지 체크

.. code-block:: python

    if ser.in_waiting == 1:
        receive = ser.read()
        if receive[0] == 1:
            print("spi communication complete")
            readMode = 0
        else:
            print("error! something wrong between arduino and chip")
            print(receive[0])
            exit()

:step6: 모두 정상이면 step3으로 돌아가 반복
