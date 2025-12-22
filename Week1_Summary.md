# Scapy-CAN Study - Week 1

## 1. 환경 설정 (Environment Setup)
실습을 위해 Python 및 Scapy 라이브러리를 설치하고 버전을 확인합니다.

```
# 시스템 패키지 업데이트
sudo apt update
sudo apt upgrade -y

# Python3 및 pip 설치
sudo apt install python3 python3-pip -y

# Scapy 설치 (APT 패키지 매니저 사용)
sudo apt install python3-scapy -y

# Scapy 설치 (pip 사용 - 최신 버전)
pip3 install scapy

# 설치 확인 (Scapy 버전 출력)
python3 -c "import scapy.all as sc; print(sc.__version__)"
```

## 2. Scapy 개념 정리 (Theory)
Scapy란?
Python 기반의 패킷 조작 및 분석 라이브러리입니다. 패킷을 생성(Generation), 분석(Analysis), 스니핑(Sniffing) 할 수 있는 강력한 도구입니다.

핵심 개념: Raw Packet vs Normal Packet
일반적인 네트워크 통신 (Normal Packet): OS(운영체제)가 자동으로 TCP/UDP 헤더 등을 생성하고 관리합니다. 사용자가 세부적인 헤더를 직접 건드리기 어렵습니다.

Scapy의 방식 (Raw Packet): Scapy는 Raw Socket을 사용합니다.

Raw Socket: OS의 네트워크 스택을 거치지 않고, 사용자가 직접 IP, TCP, UDP, ICMP 등의 헤더를 한 땀 한 땀 구성하여 보낼 수 있게 해주는 API입니다.

즉, Scapy를 사용하면 사용자가 직접 커스텀한 패킷(Raw Packet)을 생성하여 전송할 수 있습니다.

요약: Scapy는 OS가 해주는 일을 사용자가 직접 제어할 수 있게 하여, 보안 테스트나 프로토콜 분석에 용이합니다.

## 3. Git & GitHub 실습 (Workflow)
스터디원(inhwan, minseo, junhee) 각자의 브랜치를 생성하고 과제를 제출하는 과정입니다.

STEP 1: 브랜치 생성 및 이동
새로운 브랜치를 만들고 동시에 해당 브랜치로 이동합니다.

### 형식: git checkout -b [브랜치이름]
git checkout -b inhwan
STEP 2: 과제 제출 (Push)
작업한 코드를 스테이징하고 커밋한 뒤, 원격 저장소(Remote Repository)로 보냅니다.

### 1. 변경된 모든 파일 스테이징
git add .

### 2. 커밋 메시지 작성 (예: inhwan: week1 실습 제출)
git commit -m "inhwan: week1 실습 제출"

### 3. 원격 저장소로 푸시
### 형식: git push origin [브랜치이름]
git push origin inhwan
STEP 3: Pull Request (PR) 생성
코드를 main 브랜치에 합치기 위해 승인 요청을 보냅니다.

GitHub 저장소 페이지로 이동합니다.

상단에 뜬 Compare & pull request 초록색 버튼을 클릭합니다.

제목 작성: (예: inhwan: week1 제출)

내용 작성: 간단한 제출 코멘트 작성 (예: "inhwan week1 과제 제출합니다.")

우측 Reviewers에서 리뷰어 지정 (선택 사항)

하단의 Create pull request 버튼 클릭하여 완료
