> UDP : 데이터그램을 사용하여 통신하는 비연결형 프로토콜이다.
> 1. connectionless and unreliable data transfer : 연결을 설정하지 않으므로 데이터의 손실이 발생해도 오류 복구 메커니즘이 없다. unreliable을 해결하고 싶다면 application layer에서 RTP를 이용해 순서를 맞춰주고 손실된 것을 회복해줄 수 있다.
> 2. unordered delivery : 데이터는 순서대로 도착하지 않을 수 있다.
> 3. fast : 연결 설정에 따른 지연이 없어서 데이터를 빠르게 전송할 수 있다.
> 4. less traffic sent across the network : 부가적인 제어 정보가 적어서 불필요한 트래픽이 적다.
> 5. low overhead : TCP 헤더는 보통 20바이트이다. TCP 헤더에 비해 UDP헤더는 8바이트이므로 헤더의 오버헤드가 적다.
<br>
# Checksum 
- architecture
<br>&nbsp;1) pseudo header : network layer의 정보를 가져와서 가상의 헤더이다.
    - zero : 0을 넣는다
    - protocol : TCP(6), UDP(17)
    - UDP length : header + data길이
<br>&nbsp;2) UDP header
<br>&nbsp;3)UDP data : UDP data가 홀수로 끝나는 경우는 16bit를 맞춰주기 위해서 한 bit를 padded시킨다.

- operation method
<br>&nbsp;1) pseudo header + UDP datagram(header + data)에 대해서 16bit 단위로 나눈다.
<br>&nbsp;2) 16bit로 나눈 것들을 모두 더한다.
<br>&nbsp;3) 16bit를 넘어가는 carry를 더한다.
<br>&nbsp;4) 결과에 one’s complement를 한다
<br>&nbsp;5) 0이면 오류가 아니고 0이 아니면 오류이다.


1. **Pseudo Header (가상 헤더):** Network layer의 정보를 가져와서 가상의 헤더를 형성합니다.
    
    - Zero: 0을 넣습니다.
    - Protocol: TCP(6) 또는 UDP(17)를 나타냅니다.
    - UDP Length: UDP 헤더와 데이터의 길이를 더하여 넣습니다.
2. **UDP Header (실제 헤더):** UDP 프로토콜의 헤더를 사용합니다.
    
3. **UDP Data (실제 데이터):** UDP 데이터가 홀수 길이로 끝나는 경우, 16비트를 맞추기 위해 한 비트를 padded합니다.
    

**Checksum Operation Method:**

1. **Pseudo Header + UDP Datagram (Header + Data):** Pseudo Header와 UDP Datagram을 합하여 16비트 단위로 나눕니다.
    
2. **16비트로 나눈 값들을 모두 더합니다.**
    
3. **16비트를 넘어가는 carry를 더합니다.**
    
4. **결과에 One's Complement를 적용합니다.** One's Complement는 비트를 반전시키는 연산입니다.
    
5. **결과가 0이면 오류가 없으며, 0이 아니면 오류가 있습니다.**