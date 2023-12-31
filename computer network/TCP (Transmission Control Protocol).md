> TCP : 두 호스트를 연결하고 바이트 스트림을 교환하게 해주는 프로토콜이다.  
> 1. reliable transport & in-order delivery : sender가 보낸 segment이 정상적으로 receiver에게 도착했는지 acknowledgement를 사용해서 알 수 있으므로 reliable하다. 그리고 segment가 순서대로 도착하지 않아도 sequence number를 사용해 순서를 맞출 수 있다. 
> 2. point-to-point : sender와 receiver간에 1대 1로 정보를 주고 받는다.
> 3. full duplex service : 양방향 통신이 가능하다.
> 4. pipelined : 여러 segment가 동시에 전송되어 대기 중인 data가 없을 때까지 기다리지 않고, segment를 연속해서 보낼 수 있다.
    - GBN와 같이 acknowledgement를 안받은 가장 오래된 segment에 대해 timer를 구동한다
    - SR과 같이 receiver에 buffer가 있어 timeout된 segment만 재전송한다.


# 1. TCP : 3 way handshake
TCP에서는 `3-way handshake`를 통해 연결을 설정한다. 

- Establishing TCP Connection
  <br><img width="558" alt="threewayhandshake" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/880fe4d1-9f61-4dfd-a93f-42e4184382de">
<br>&nbsp;1) [client : CLOSED -> SYNSENT] client는 server에 접속을 요청하기위해 SYN을 보낸다.
<br>&nbsp;2) [server : LISTEN → SYN RCVD] server는 client가 보낸 요청에 대한 ACK와 연결을 위한 SYN을 보낸다
<br>&nbsp;3) [client : SYNSENT → ESTABLISHED]  client는 server가 보낸 ACK을 받고 연결이 되었는다는 것을 알수있다. 그리고 server가 보낸 SYN에 대한 ACK을 보낸다.
<br>&nbsp;4) [server : SYN RCVD → ESTABLISHED] client가 보낸 ACK을 받고 연결이 되었는다는 것을 알 수 있다.

	**(*)TCP connection일때 SYN의 sequence number를 랜덤하게 하는 이유는?**
	SYN의 sequence number를 예측할 수 있다면 attacker가 client인척하고 host에게 요청을 보내 server와 연결할 수 있다. 이후에는 attacker가 악의적인 데이터를 전송해 server애 피해를 줄 수 있다.

<br>

- Closing TCP Connection
  <br><img width="558" alt="closing" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/9ff0fcb9-8a7c-49fc-b2b1-bfd324dd68ac">
<br>&nbsp;1) [client : ESTABLISHED → FIN_WAIT_1] 연결을 끊기위해 server로FIN을 보낸다. 
<br>&nbsp;2) [server : ESTABLISHED → CLOSE_WAIT FIN] 요청에 대한 ACK를 보내고 모든 data가 전달될때까지 기다린다.
<br>&nbsp;3) [server : CLOSE_WAIT → LAST_ACK] data를 다 보내고 연결을 끊기위해 client에게 FIN을 보낸다. 
<br>&nbsp;4) [client : FIN_WAIT_2→ TIME_WAIT → CLOSED] server로 부터온 FIN메세지에 대한 ACK을 보내고 2MSL시간동안 기다린 뒤 CLOSED 상태가 된다.
<br>&nbsp;5) [server : LAST_ACK → CLOSED ] client로 부터 ACK를 받으면 CLOSED상태가 된다.

	**(*)MSL을 설정하는 이유는?**
	 MSL가 없으면 client가 보낸 ACK이 손실 된 경우 server의 timer가 timeout이 되어 다시 FIN을 보내도 응답할 client가 없어서 리소스를 낭비하게 된다.
<br>

# 2. GO BACK N이란?
>GO BACK N
>1. timeout & retransmission : 지정한 시간안에 응답이 안오면 재전송을 한다.
>2. pipelined protocols : ACK를 받지 않아도 주어진 범위(window) 안에서는 segment을 여러개 보낼 수 있다.
>3. cumulative ACK : 순서대로 수신하여할 다음 segment의 sequence number를 ACK number로 지정한다.
>4.  sliding window : 윈도우 내에 있는 일부 패킷들을 전송하고, 이에 대한 ACK을 받으면 윈도우를 이동시켜서 더 많은 패킷을 전송할 수 있다. 
<br>
<img width="615" alt="GOBackN" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/4c7a8d17-8f81-4a2d-8010-42c1f847b408">

- [sender]
<br>&nbsp;1) window size가 N일때 N개의 segment은 ACK없이 보낼 수 있다.
<br>&nbsp;2) 가장 오래 ACK를 받지않은 segment에 timer를 적용한다.
<br>&nbsp;3) timeout전에 ACK가 오면 sliding window를 하고 다음 segment을 보낸다. timeout이 발생하면 해당 segment이후에 전송되었던 모든 segment들을 모두 재전송하고 window 범위내에서 전송할 segment들을 계속 전송한다.

- [receiver]
<br>&nbsp;1) 다음 segment의 sequence number를 ACK number로 보낸다
<br>&nbsp;2) 순서대로 오지 않은 segment에 대한 ACK는 보내지 않고 loss된 segment에 대한 ACK을 보낸다.

- 장점 : 많은 양의 segment 전송이 가능하다.
- 단점 : timeout이 되면 해당 segment 이후에 전송되었던 모든segment을 재전송하므로 불필요한 재전송이 발생한다.
<br>

# 3. Selective repeat(SR)이란?
>Selective repeat(SR)
>1.  timeout & retransmission : 지정한 시간안에 응답이 안오면 재전송을 한다.
>2. pipelined protocols : ACK를 받지 않아도 주어진 범위(window) 안에서는 segment을 여러개 보낼 수 있다.
>3. ACK : 수신한 segment의 sequence number를 ACK number로 지정한다.
>4. sliding window : 윈도우 내에 있는 일부 패킷들을 전송하고, 이에 대한 ACK을 받으면 윈도우를 이동시켜서 더 많은 패킷을 전송할 수 있다. 
>5. buffer : receiver에서 수신한 segment을 임시로 저장한다.
<br>
<img width="667" alt="SR" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/b53f826b-907e-46a9-ab47-ffe057b0a231">
- [sender]
<br>&nbsp;1) application에서 data가 내려오면 sequence number를 부여한다. window내에 있는 segment을 receiver에게 전송한다.
<br>&nbsp;2) 모든 segment에 대해 timer를 구동한다.
<br>&nbsp;3) ack가 도착했는데 만약 window의 맨앞 segment이라면 sliding window 을 한다.
<br>&nbsp;4)timeout된 segment만 재전송하고 window 범위 내에서 전송할 segment들을 계속 전송한다.

- [receiver]
<br>&nbsp;1) 다음 segment의 sequence number를 ACK number로 보낸다
<br>&nbsp;2) 순서대로 오지 않은 segment에 대한 ACK는 보내지 않고 loss된 segment에 대한 ACK을 보낸다.

- 장점 : buffer를 사용하므로 불필요한 재전송이 발생하지 않는다.
- 단점 : buffer를 사용하므로 속도가 느릴 수 있다.




# 4. Congestion Control

# 5. Flow Control

