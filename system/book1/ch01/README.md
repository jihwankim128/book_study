## 컴퓨터 구조를 학습하는 이유 (개발자의 관점)

- 개발 환경과 운영 환경에서 동일한 코드가 동작하지 않을 수 있으므로 대비가 필요하다.
- 운영 환경의 컴퓨터 스펙을 정하고 성능, 용량, 비용 등을 고려해야한다.

위 두 가지 상황에서 컴퓨터 구조는 필수 지식이 된다.

## 컴퓨터 구조

- SW
  - 이진 데이터 (0, 1)
  - 데이터(정보)와 명령어가 됨
- HW
  - Main Board (System Bus를 통해 통신)
    - CPU (Central Processing Unit)
      - ALU (Arithmetic Logic Unit)
      - CU (Control Unit)
      - Registers
    - Main Memory
      - RAM (Random Access Memory)
      - ~~ROM (Read Only Memory)~~: 현대에 거의 안쓰임
  - Secondary Storage
  - I/O Device

## Memory

* 명령어와 데이터를 저장하는 부품으로 컴퓨터가 실행되려면 무조건 메모리에 저장되어야 함.
  * 명령어와 데이터는 0101010과 같이 이진수로 저장됨
* 메모리의 명령어와 데이터에 접근하기 위해 메모리 내부에서 논리적인 주소(Address)로 관리

## CPU

* 메모리에 저장된 명령어를 읽고, 해석하고 실행하는 실제 동작을 하는 장치
* ALU: 계산을 하는 역할
* 레지스터: 임시 저장 장치 
* 제어장치: 제어 신호(control signal)을 통해 제어하고 명령어를 해석
  * 메모리에 저장된 명령어와 데이터를 -5v, +5v 와 같은 식으로 0, 1을 표현하는 신호를 발생하면서 명령어를 실행

> CPU와 Memory의 간단한 동작 과정

연산 과정  
RAM -> CPU Instruction Register -> CU -> memory address -> CPU Temp Register -> ALU -> CPU Result Register

저장 과정  
RAM -> CPU Instruction Register -> CU -> memory address -> save

## 보조기억장치

* 메모리의 단점을 보완하는 장치
  * 메모리는 가격이 비싸고 저장 용량이 적다
  * 휘발성 (전원이 꺼지면 데이터가 날라감)
* 전원이 꺼져도 데이터가 보존된다. (바탕화면에 파일이 남아있는 그 원리)

## 메인보드와 시스템 버스

* 컴퓨터 핵심 부품을 담는 보드로 보조기억장치, 입출력장치를 제외하고 메인보드에 있다.
* 시스템 버스는 각 부품 간 신호를 주고 받는 중요한 통로
  * 주소버스, 데이터버스, 제어버스로 구성

> 시스템 버스를 포함한 처리 과정

연산 과정  
CPU 제어 신호 (제어 버스) -> RAM 메모리 접근 (주소 버스) -> 메모리 정보를 CPU Register에 저장 (데이터 버스)

저장 과정 
CPU Register의 레지스터 통로 연결 (데이터 버스) -> 저장할 RAM 주소 접근 (주소 버스) -> CPU 메모리 쓰기 신호 (제어 버스)