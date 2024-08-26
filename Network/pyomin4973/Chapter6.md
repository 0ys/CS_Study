6.3 Multiple Access Links and protocols

- Link layer는 network interface card에 구현되어 있다. firm-ware
- 링크레이어에서 제공하는 기능 중 collision을 피해가는 것이있다
    - multiple access links에서의 protocols은 탈집중화되고 간단해야한다
    - 링크레이어에서의 MAC 목적: 링크 bandwidth가 R인 상황에서
        - when one node wants to transmit이면 전체 bandwidth 사용
        - 여러개의 node가 사용을 원할 땐, 공평하게 1/N으로 사용
        
- Mac 프로토콜은 channel partitioning 과 random access 방법등이 있다
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/084bdf6b-4d4f-4297-b821-4c0b6dd6aeca/image.png)
    
- Channel partitioning MAC protocols-TDMA: time division multiple access, access to channel in rounds여서(round로 채널에 접근하게해서 시간을 나눠서 multiple access를 하게해서) 충돌은 나지 않지만 사용하지 않는 시간에 대해서 나머지 slot이 남는 단점
- Channel Partitions MAC Protocols-FDMA: fequency division multiple access.(주파수를 나누어서 multiple access 를 하도록 함)

- Random access protocols: 충돌이 발생해서 탐지가 필요하다. 많이 사용되고 회복방식에 대한 명시가 필요하다.
    - CSMA: carrier sense multiple access. 보내기전에 들어보고(carrier sense를 해서) 없으면 보낸다. listen before transmit. if channel sensed idel: transmit entire frame. If channel sensed busy: defer transmission.
        - collisions는 여전히 생길 수 있다. propagation delay로 인해 두 노드가 서로의 전송을 듣지 못할 수도 있다. 충돌이 발생하면 전체 패킷 전송 시간이 낭비된다. (LAN선 상의 전자기파 제한 속도 때문에 캐리어센스 후에 상대편의 노이즈가 도착하면 충돌 가능하다)
        - 충돌 damage 최소화: CSMA/CD
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/3fa3e293-fd79-4aa8-9d20-78a937cb25e5/image.png)
            
    - CSMA/CD  : collision탐지한 순간 전송을 멈춰서 한 프레임을 모두 전송하지 않는것.
        - NIC가 network layer에서 데이터그램 받고 frame을 만든다. →NIC가 cs했을 때 idle하면 frame 보내기 시작. busy면 기다렸다가 idle이면 전송 →(여기까지 CSMA)
        - NIC가 다른 전송을 탐지하지 않고 전체 프레임을 보냈다면 NIC는 이 프레임과 관계가 끝난것이다. 반면에 NIC가 다른 전송을 자신의 프레임을 전송하고 있을 시기에 들으면 abort를 하고 jam signal(충돌시그널을 보낸다.)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/f2458c0e-4550-40c6-a482-0b8b2d879957/image.png)
    
    - 충돌 탐지하면 random timer 돌려서 재전송: random 폭이 좁아야 빨리 전송됨. 첫 충돌시 작은 범위에서 충돌이 계속나면 큰 범위로 폭을 넓히는데 binary exponential로 늘려나간다. 또 호스트 많을 수록 충돌이 많이 일어남.
        - 하지만 무선 상황에서는 충돌감지가 쉽지 않다. 외부로서의 노이즈를 차단할 수 있는 환경이 아니기 때문이다. 이건 7장.

6.4 Switched Local Area Network

- 이더넷: 컴퓨터 네트워크에서 데이터 전송을 위한 표준 기술로, 로컬 영역 네트워크(LAN, Local Area Network)에서 주로 사용됩니다. 이더넷은 데이터를 프레임이라는 단위로 묶어 네트워크 상의 다른 장치에 전달하며, 네트워크 케이블과 스위치, 라우터 등과 함께 작동합니다.
    - 즉 유선 케이블 상의 MAC 미디엄 엑세스 프로토콜. 이더넷의 물리적 위상구조로는 bus등이 있는데 요즘에는 중간에 switch를 둔 star 모양.
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/3a0c6fd1-3c2a-44da-86a0-f5de21120987/image.png)
        
- ethernet frame structure: data field에 IP 패킷이 들어간다. 링크 layer에서 사용하는 mac addr, dst address, src address도 포함되어있다.
- 이더넷은 MAC protocol로 CSMA/CD를 사용한다.
- collision이 생겼는데도 탐지가 안되면 제대로 전송되지 않을 수 있다. A collision happens in Ethernet But is not detected at MAC layer.(CSMA/CD 가 MAC layer의 ACKs를 쓰지않기 때매 나타나는 문제)
    - A의 프레임이 너무 짧으면 충돌 감지가 안되는 것이 있다. 만약에 A가 프레임을 전송하는 중에 충돌신호가 들어온다면 충돌함을 알고 재전송할 수 있다.하지만 그전에 A에서 프레임이 짧아서 충돌신호가 들어오기전에 전송이 끝나면 A는 충돌이 된지 모른다
    - 그래서 LAN선의 최대 길이도 감안해서 frame사이즈의 최소사이즈가 정해져있다. G에서 보낸 것이 충돌되어 탐지되기 전에 A가 프레임 전송을 끝내면 충돌감지가 안됨. 그래서 패딩을 붙이거나 등으로 최소사이즈 채움.
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/127fe647-a11a-4fcb-bde3-56b6b8c87bb2/image.png)
        

- LANs: LAN(Local Area Network, 로컬 영역 네트워크)은 비교적 작은 지리적 범위 내에서 네트워크 장치들을 연결하는 컴퓨터 네트워크입니다. each adapter on LAN has unique LAN address.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/5640277e-02b4-4e25-9eec-2c105ea92174/image.png)
    
    - mac addr는 네트워크인터페이스 카드가 생성되는 순간 제조사에서 찍히는 것처럼, (IP주소와 달리) 바뀌지 않음. 48BIT라서 16진수로 끊어서 표현.
- ARP: address resolution protocol.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/2aee3e78-c1c7-470d-87a0-023c57f7c92c/image.png)
    
    - how to determine interface’s MAC address, knowing its IP address → IP주소로 MAC주소를 얻어오기 위한 프로토콜이 ARP이다
    - 이더넷 프레임의 구성요소 중 type field에는 IP 패킷인지 ARP query인지를 명시함. ARP query에는 궁금해하는 interface의 IP주소(e.g., 1.1.1.1)이 담김.
    - IP주소에 해당하는 것만 ARP query에 반응한다. ARP response를 담아서 A한테 알려주게 된다. A는 알게된 정보를 ARP table에 작성한다.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/030d7ad5-cb46-41ea-9074-e962b6bea8ad/image.png)
    
    - Gateway Router는 봉투뜯어서 IP패킷받고 forwarding을 위해 라우터에 있는 포워딩 테이블 참고해서 next에 해당하는 IP주소 찾음 → IP주소에 해당하는 MAC 주소 얻기 위해서 ARP table 참조. 즉 패킷 받은 후에 테이블 2번 참조해서 dst addr에 적을 수 있다.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/69bb981d-96e8-4321-a446-f7a96c49db71/image.png)
    
    - A가 생성한 IP 패킷은 구글에 도착할 때까지 크게 변하지 않음. IP패킷을 담은 Frame의 src와 dst가 바뀌게 됨.
- Switch: multiple simultaneous transmission. 동시에 다수의 transmission을 가능하게 한다. A에서 A’로, B에서 B’로의 전송을 충돌없이 동시에 할 수 있도록 한다.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/a1d5d688-600f-4d64-8242-3182612da247/image.png)
    
    - A에서 A’으로 가고싶을 때 어떤 인터페이스로 가는지를 결정하는 방법은,  각 스위치에 스위치테이블이 있어서 호스트가 어떤 인터페이스에 위치하는지를 알 수 있다. → self learning으로 학습
        - 스위치는 어떤 인터페이스로 호스트에 도달할 수 있는 지를 스스로 학습하는데, 프레임이 본인한테 도착하여 전달되면 스위치는 sender의 위치를 배운다.
