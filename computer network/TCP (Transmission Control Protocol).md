> TCP : 두 호스트를 연결하고 데이터 스트림을 교환하게 해주는 프로토콜이다.  
> 1. reliable transport & in-order delivery : sender가 보낸 packet이 정상적으로 receiver에게 도착했는지 acknowledgement를 사용해서 알 수 있으므로 reliable하다. 그리고 packet이 순서대로 도착하지 않아도 sequence number를 사용해 순서를 맞출 수 있다. 
> 2. point-to-point : sender와 receiver간에 1대 1로 정보를 주고 받는다.
> 3. full duplex service : 양방향 통신이 가능하다.
> 4. pipelined
    - GBN와 같이 acknowledgement를 안받은 가장 오래된 segment에 대해 timer를 구동한다
    - SR과 같이 receiver에 buffer가 있어 timeout된 segment만 재전송한다.


# 1. TCP : 3 way handshake
TCP에서는 `3-way handshake`를 통해 연결을 설정한다. 

- Establishing TCP Connection
	<img width="558" alt="threewayhandshake" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/880fe4d1-9f61-4dfd-a93f-42e4184382de">
1) [client : CLOSED -> SYNSENT] client는 server에 접속을 요청하기위해 SYN을 보낸다.
2) [server : LISTEN → SYN RCVD] server는 client가 보낸 요청에 대한 ACK와 연결을 위한 SYN을 보낸다
3) [client : SYNSENT → ESTABLISHED]  client는 server가 보낸 ACK을 받고 연결이 되었는다는 것을 알수있다. 그리고 server가 보낸 SYN에 대한 ACK을 보낸다.
4) [server : SYN RCVD → ESTABLISHED] client가 보낸 ACK을 받고 연결이 되었는다는 것을 알 수 있다.

	**TCP connection일때 SYN의 sequence number를 랜덤하게 하는 이유는?**
	SYN의 sequence number를 예측할 수 있다면 attacker가 client인척하고 host에게 요청을 보내 server와 연결할 수 있다. 이후에는 attacker가 악의적인 데이터를 전송해 server애 피해를 줄 수 있다.



- Closing TCP Connection
  	<img width="559" alt="closing" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/9ff0fcb9-8a7c-49fc-b2b1-bfd324dd68ac">
1) [client : ESTABLISHED → FIN_WAIT_1] 연결을 끊기위해 server로FIN을 보낸다. 
2) [server : ESTABLISHED → CLOSE_WAIT FIN] 요청에 대한 ACK를 보내고 모든 data가 전달될때까지 기다린다.
3) [server : CLOSE_WAIT → LAST_ACK] data를 다 보내고 연결을 끊기위해 client에게 FIN을 보낸다. 
4) [client : FIN_WAIT_2→ TIME_WAIT → CLOSED] server로 부터온 FIN메세지에 대한 ACK을 보내고 2MSL시간동안 기다린 뒤 CLOSED 상태가 된다.
5) [server : LAST_ACK → CLOSED ] client로 부터 ACK를 받으면 CLOSED상태가 된다.

	**MSL을 설정하는 이유는?**
	 MSL가 없으면 client가 보낸 ACK이 손실 된 경우 server의 timer가 timeout이 되어 다시 FIN을 보내도 응답할 client가 없어서 리소스를 낭비하게 된다.


# 2. GO BACK N이란?


# 3. Selective repeat(SR)이란?

# 4. Congestion Control

# 5. Flow Control

