# TCP 3-Way-HandShake & 4-Way-HandShake
## TCP??
TCP는 장치들 사이에 논리적인 접속을 성립(establish)하기 위하여 연결을 설정하여 **신뢰성을 보장하는 연결형 서비스이다.** 

## 3-way-handshake??

>TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 **연결을 설정(Connection Establish)** 하는 과정

- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작되기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다. 
- 즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다. 
	- A 프로세스(Client)가 B 프로세스(Server)에 연결을 요청 
	<img width="474" alt="스크린샷 2020-12-01 오후 6 03 32" src="https://user-images.githubusercontent.com/44199159/100719148-97b79500-33ff-11eb-86c0-c6deb13b908a.png">
	
	1. A -> B : SYN
		
		- 접속 요청 프로세스 A가 연결 요청 메세지 전송(SYN)
		- 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 넘버로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다. 
		- PORT 상태 -> B : LISTEN, A : CLOSED 
	2. B -> A : SYN + ACK 
		- 접속 요청을 받은 프로세스 B가 요청을 수락했으며, 접속 요청 프로세스인 A도 포트를 열어 달라는 메세지를 전송(SYN + ACK)
		- 수신자는 Acknowledge Number 필드를 (Sequence Number + 1)로 지정하고, SYN과 ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다. 
		-  PORT 상태 - B : SYN_RCV, A : CLOSED 
	
	
	3. A -> B : ACK
		- PORT 상태 - B : SYN_RCV, A : ESTABLISHED 
		- 마지막으로 접속 요청 프로세스가 A가 수락 확인을 보내 연결을 맺음(ACK) 
		- 이떄, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다. 
		- PORT 상태 - B : ESTABLISHED, A : ESTABLISHED 
	

## 4-way handshake ??
> TCP **연결을 해제(Connection Termination)** 하는 과정 

- A 프로세스(Client)가 B 프로세스(Server)에 연결 해제를 요청 
<img width="469" alt="스크린샷 2020-12-01 오후 6 20 11" src="https://user-images.githubusercontent.com/44199159/100720857-ef570000-3401-11eb-93b4-ae1c08bcdf07.png">
	1. A -> B : FIN
		- 프로세스 A가 연결을 종료하겠다는 FIN 플래그를 전송 
		- 프로세스 B가 FIN 플래그로 응답하기 전까지 연결을 계속 유지 
	2. B -> A : ACK
		- 프로세스 B는 일단 확인 메시지를 보내고 자신의 통신이 끝날 때까지 기다린다. (TIME_WAIT 상태) 
		- 수신자는 Acknowledge Number 필드를 (Sequence Number + 1)로 지정하고, ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다. 
		- 그리고 자신이 전송할 데이터가 남아있다면 이어서 계속 전송한다. 
	3. B -> A : FIN
		- 프로세스 B가 통신이 끝났으면 연결 종료 요청에 합의한다는 의미로 프로세스 A에게 FIN 플래그를 전송 
	4. A -> B : ACK
		- 프로세스 A는 확인했다는 메세지를 전송 

## [참고자료]  
### *PORT 상태 정보* 
- CLOSED : 포트가 닫힌 상태 
- LISTEN : 포트가 열린 상태로 연결 요펑 대기 중 
- SYN_RCV : SYNC 요청을 받고 상대방의 응답을 기다리는 중 
- ESTABLISHED : 포트 연결 상태 

### *플래그 정보*
- TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하며, 각각의 bit는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다.
	- 즉, 해당 위치의 bit가 1이면 해당 패킷이 어떠한 내용을 담고 있는 패킷인지를 나타낸다.
- SYN(Synchronize Sequence Number) / 000010
	- 연결 설정. Sequence Number를 랜덤으로 설정하여 세션을 연결하는 데 사용하며, 초기에 Sequence Number를 전송한다. 
- ACK(Acknowledgement) / 010000
	- 응답 확인. 패킷을 받았다는 것을 의미한다.
	- Acknowledgement Number 필드가 유효한지를 나타낸다.
	- 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 첫 번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정된다고 생각할 수 있다.
- FIN(Finish) / 000001
	- 연결 해제. 세션 연결을 종료시킬 때 사용되며, 더 이상 전송할 데이터가 없음을 의미한다.        
	
	
	
