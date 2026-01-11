# CPU 작동원리 

## ALU

* A + B = C 가 있으면
  * A(피연산자), B(피연산자), C(결과값)는 레지스터
  * (+)는 제어장치로부터 전달되는 제어 신호
  * 결과(=)에 대한 양수, 음수, 레지스터 한계 초과 (overflow) 등을 플래그 레지스터에 전달

## 플래그

* 연산 결과에 대한 추가적인 상태 정보를 구성
* 구성

|부호|제로|캐리| 오버플로우 |인터럽트|슈퍼바이저|
|--|--|--|-------|--|--|
|0|0|0| 0     |0|0|

## 제어장치

* 클럭 신호, 해석할 명령어, 플래그 값, 제어 버스의 제어 신호를 전달받음
* CPU 내부와 외부로 제어 신호를 전달함
  * 내부: ALU와 Register
  * 외부: 메모리, 외부장치 등

# 레지스터

## PC (Program Count)
* 다음 처리할 명령어의 주소를 저장
* Instruction pointer 라고도 함

## IR (Instruction Register)
* 방금 메모리에서 읽은 명령어를 저장

## MAR (Memory Address Register)

* 메모리 주소 정보를 가짐

## MBR (Memory Buffer Register)

* 메모리에 R/W 할 정보를 저장
* MDR (Memory Data Register) 라고도 함

## General purpose register

* 메모리와 주소를 모두 저장할 수 있는 레지스터 (변수)

## Flag Register

* 앞서 나온 것 CPU 상태에 대한 부가적인 정보

## 스택 주소 지정 방식

* 스택 포인터와 스택 레지스터를 활용한 방법
* 스택 영역으로 함수를 사용할 때 마다 현재 함수가 얼마나 스택이 쌓였는지 저장
* 함수와 유사한 방법

## 변위 주소 지정 방식 (displacement addressing mode)

* 특정 레지스터의 값과 오퍼랜드 필드를 더해 유효주소를 얻는 방법

### 상대 주소 지정 방식 (relative addressing mode)

* 오퍼랜드(값) + 프로그램 카운터 -> 유효주소
* 현재 PC + 값(-3) -> 현재 Memory Address - 3
* 현재 PC + 값(+3) -> 현재 Memory Address + 3
* if 문과 유사한 방법 

### 베이스 레지스터 주소 지정 방식 (base-register addressing mode)

* operand + base register -> 유효주소
* 상대 주소 지정 방식과 같이 base register 부터 operand 만큼 떨어진 처리
* for 문에서 continue 나 break 할 때, 혹은 함수 처리 할 때 CPU 마다 다르게 설정하는 듯

# 명령어 사이클과 인터럽트

* 시스템 개발자, 보안 등 백엔드와는 연관성이 낮음 (읽어보기만 하기)