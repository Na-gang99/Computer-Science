> TCP : 두 호스트를 연결하고 데이터 스트림을 교환하게 해주는 프로토콜이다.  
> 1. ==reliable transport & in-order delivery== : sender가 보낸 packet이 정상적으로 receiver에게 도착했는지 acknowledgement를 사용해서 알 수 있으므로 reliable하다. 그리고 packet이 순서대로 도착하지 않아도 sequence number를 사용해 순서를 맞출 수 있다. 
> 2. ==point-to-point== : sender와 receiver간에 1대 1로 정보를 주고 받는다.
> 3. ==full duplex service== : 양방향 통신이 가능하다.
> 4. ==pipelined==
    - GBN와 같이 acknowledgement를 안받은 가장 오래된 segment에 대해 timer를 구동한다
    - SR과 같이 receiver에 buffer가 있어 timeout된 segment만 재전송한다.

# 1. TCP : 3 way handshake
TCP에서는 `3-way handshake`를 통해 연결을 설정한다. 

- Establishing TCP Connection![[threewayhandshake.png]]
|client|server|
|--|--|
|1. CLOSED → SYNSENT client가 server에게 연결을 위해 syn을 보낸다.|1. LISTEN → SYN RCVD server는 항상 켜있는 상태로 있다가 client가 보낸 메세지에 대한 ack와 연결을 위한 syn을 보낸다


- Closing TCP Connection







# 2. GO BACK N이란?
# 3. Selective repeat
# 4. Congestion Control
# 5. Flow Control