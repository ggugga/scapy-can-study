Replay Attack
이 실습은 터미널 창(Tab)을 3개 열어서 진행

## [창 1] 피해자(ECU) & 모니터링

이 창은 차량의 내부 네트워크 상황을 지켜보는 '계기판' 역할

![](./images/replay1.png)

rm candump-*.log는 실습환경 초기화

modprobe: 기능 활성화 

add: 장치 생성 

set up: 전원 켜기 




## [창 2] 해커 녹음 시작

![](./images/replay2.png)

candump -l vcan0: 로깅 옵션(-l)을 사용하여 녹음 내용을 로그 파일로 저장




## [창 3] 운전자가 문 열림 신호 발생시켰다고 가정

![](./images/replay3.png)

정상적인 문 열림 신호를 3번 보내는 과정

![](./images/replay4.png)

[창 2]는 그 신호들을 녹음중

![](./images/replay5.png)

[창 1]는 운전자의 신호를 받고 있음

![](./images/replay7.png)

녹음을 중단(Ctrl+C)하고 ls로 파일 확인 후 공격(canplayer) 실행

![](./images/replay8.png)

[창 1]는 운전자의 신호가 아닌 녹음된 내용을 정상신호로 인식하고 있음

재전송 공격 성공!

##과제
재전송공격 과정 1~3줄 요약 정리
