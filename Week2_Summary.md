# Scapy-CAN Study - Week 2

## 1. Scapy 패킷 생성 실습 (IP / TCP / ICMP)

### 인터랙티브 모드 진입
sudo scapy

### ICMP 패킷 전송
p = IP(dst="8.8.8.8") / ICMP()   # type=8 (echo-request)
p.show()
send(p)

### TCP SYN 패킷 전송 (정상 포트)
p = IP(dst="google.com") / TCP(dport=80, flags="S")
p.show()
send(p)

### TCP SYN 패킷 전송 (비정상 포트)
p = IP(dst="example.com") / TCP(dport=9999, flags="S")
send(p)


---

## 2. CAN 개념 정리 (Controller Area Network)

### CAN이란?
Controller Area Network  
자동차 내부 ECU(Electronic Control Unit) 간 통신 네트워크

### CAN 메시지 구조
1. Identifier (ID)
- 주소가 아님
- 메시지 종류 및 우선순위 표현

2. DLC (Data Length Code)
- 데이터 길이 (0~8 byte)

3. Data
- 실제 전달 데이터


---

## 3. CAN 패킷 인젝션 (Injection)

패킷 전송 행위  
공격 관점: 정상 ECU인 것처럼 메시지를 위조해 삽입


---

## 4. 가상 CAN 환경 구축 (vcan)

### 커널 모듈 로드
sudo modprobe vcan

### vcan0 인터페이스 생성
sudo ip link add dev vcan0 type vcan

### vcan0 인터페이스 활성화
sudo ip link set up vcan0

### 인터페이스 확인
ifconfig vcan0

### ip link 의미
modprobe: 기능 활성화  
add: 장치 생성  
set up: 전원 ON


---

## 5. CAN 모니터링 도구

### can-utils 설치
sudo apt install can-utils

### 패킷 실시간 확인
candump vcan0


---

## 6. Scapy CAN 패킷 생성 및 전송

### CAN 소켓 모듈 로드
load_contrib('cansocket')

### vcan0 소켓 연결
sock = CANSocket(channel='vcan0')

### CAN 패킷 생성
packet = CAN(
    identifier=0x123,
    data=b'\x11\x22\x33\x44\x55\x66\x77\x88'
)
packet.show()

### 패킷 전송 (Injection)
sock.send(packet)


---

## 7. CAN 공격 유형

Spoofing Attack  
정상 ECU 메시지를 공격자가 위조 전송

Replay Attack  
과거 정상 메시지를 그대로 재전송

Flooding Attack  
고속 반복 전송으로 ECU 마비

Diagnostic Abuse  
UDS (0x11, 0x3E) 오남용 공격


---

## 8. CAN 보안 핵심 포인트

Identifier (ID)
- 공격: ID 동일하게 맞춰 스푸핑
- 방어: ID 필터링, 화이트리스트

DLC
- 비정상 길이 → 이상 탐지 가능

Data 구조
- 공격: 비트 플립
- 방어: 비정상 값 검증

Standard vs Extended
- Standard: 11bit
- Extended: 29bit

Periodic Message
- 주기 교란 → 공격
- 주기 이상 → 탐지


---

## 9. Replay Attack 실습

### 터미널 구성
[창 1] ECU & 모니터링
candump vcan0

[창 2] 공격자 (녹음)
candump -l vcan0

[창 3] 정상 사용자 메시지 전송

### 공격 흐름
1. 정상 메시지 녹음
2. 로그 파일 생성 확인
3. canplayer로 재전송
4. ECU가 정상 메시지로 인식

### 환경 초기화
rm candump-*.log


---

## 과제: Replay Attack
