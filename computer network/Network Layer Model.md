## 0. 계층 모델

<img width="692" alt="02" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/12734d66-331f-4f41-aaa5-34833fad10e3">

- 성공적인 정보 교환을 위해서는 통신을 하는 두 개체가 같은 수의 계층을 가져야하고 각 Layer에는 동일한 protocol이 있어야한다. 그리고 상위 & 하위 계층 간에 동일한 인터페이스가 필요하다.
- Layer가 나눠져 있기 때문에 시스템을 유지보수하기 편하다. 그리고 각 Layer는 독립적으로 개발하고 업데이트 할 수 있으므로 전체 시스템의 변경이나 확장이 용이해진다.
<br>
> OSI와 TCP/IP 구조를 갖는 각각 두 end system들이 상호 데이터 교환이 불가한 이유는?
- OSI는 7 layer, TCP/IP는 5 layer이므로 layer의 개수가 일치하지 않는다
- OSI의 presentation과 session layer가 TCP/IP에는 정의되어 있지 않으므로 protocol을 일치시킬 수 없다.
- OSI와 TCP/IP는 interface 정의가 서로 다르다.
<br>

## 1. OSI(Open Systems Interconnection)
- Application Layer를 세 가지 하위 Layer(Application Layer, Presentation Layer, Session Layer)로 나눈다.
- 네트워크의 물리적인 부분을 다루는 Physical Layer와 데이터 전송을 관리하는 Data Link Layer를 별도로 구분한다.
<br>

## 2. TCP/IP
1. **TCP/IP는 총 4개의 계층으로 이루어져 있다.Encapsulation**
    - Application Layer : 사용자와 네트워크 간의 상호작용을 담당한다. 프로토콜로는 FTP(파일전송), HTTP(웹), SSH(암호화 네트워크 프로토콜), SMTP(메일전송), DNS(도메인이름 &IP주소 매핑)이 있다.
    - Transport Layer : 송신자와 수신자간의 신뢰성 있는 데이터 전송을 담당한다. 프로토콜로는 TCP, UDP가 있다.
    - Network Layer : 데이터 전송을 위해 목적지까지 경로를 설정하고 전달하기 위한 라우팅기능을 수행한다. 그리고 IP주소를 할당한다.
        - Error Detection : 데이터 전송 중에 발생할 수 있는 비트 오류나 프레임 손상을 식별하기 위해 checksum이나 CRC를 사용한다.
    - Link Layer : 장치간에 신호를 주고받는 규칙을 정한다.
        - DataLink Layer : physical 계층의 신호를 프레임 단위로 분할하고, 각 프레임에 대한 주소와 오류제어 등의 정보를 추가한다.
        - Physical Layer: 비트 단위의 데이터를 전송하기 위한 전기신호, 무선 등의 물리적인 특성을 다룬다.
        
2. **Encapsulation** : 상위 계층에서 하위 계층으로 데이터를 전달한다. 하위 계층은 전달받은 데이터를 변형할 수 없고 해당 계층의 헤더 정보를 추가하여 그 다음 계층으로 전달한다.
    
    <img width="1000" alt="03" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/636777e3-1f51-4e72-9d98-9c406d2fde44">
    
3. **Decapsulation** : 하위 계층에서 상위계층으로 PDU를 전달하며 각 계층의 헤더 부분을 제거하고 자신에게 필요한 데이터를 추출한다. 
    
    <img width="1000" alt="04" src="https://github.com/Na-gang99/Computer-Science/assets/155069538/1b6ab6ec-271f-435a-a0e2-35a9b3e114f6">
<br>
> PDU(Protocol Data Unit) : header+SDU(상위계층에서 전달한 데이터)
- 네트워크의 한 Layer에서 다른 Layer로 전달될 때 한 덩어리의 단위이다.
- 각 Layer마다 PDU를 부르는 명칭이 다르다.
