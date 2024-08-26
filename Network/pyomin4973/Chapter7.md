7.3 Wifi: 802.11 Wireless LANs

*Wireless LAN Architecture, MAC Protocol, Frame, Mobility in the Same IP Subnet, Advanced Features, Personal Area Networks: Bluetooth

- 무선 상황에서의 MAC이 wifi이다.(충돌되지 않게)
    
    
- wireless link의 특성
    - 유선과 달리, 공기를 타고가기 때문에 signal 세기가 줄어든다. 다른 MAC protocol을 사용해야한다.(CSMA/CD 적용불가) 충돌감지시 내가 말하는 소리가 크고 남이 말하는 소리가 작으면 충돌감지가 잘안된다.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/22ac4fc2-2e2c-4d91-8581-c68dc8ab30dd/image.png)
    
- Wifi : 표준 → IEEE 802.11 Wireless LAN
    - wifi 전송범위 내의 access point 랑 연결 → access point는 뒤로 스위치에 연결되어 있다. 주기적으로 broadcasting을 해서 각 디바이스에서 어떤 wifi있는지 확인할 수 있다.
    - CSMA/CA(collision avoidance): carrier sense해서 조용하면 → 잠깐 기다렸다가 sender가 프레임을 전송한다. →그 후에 receiver가 ACK를 보낸다.
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/a2f78c17-bce3-407c-b39c-bf4c31365218/image.png)
        
        - 이더넷은 충돌만 안하면 100프로 간 것이지만 Wifi에서는 충돌여부를 모르기 때문에 link-layer ACK가 있어야 전송이 확인되는 상황이다. ACK받을 때까지 재전송한다.
    - 충돌이 온전히 전해지는 상황을 개선 → RTS-CTS exchange
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/9ca8d066-cc7a-4920-a9ec-706bc5e5375c/image.png)
        
        - carrier sense 후에 RTS(ready to send- 내가 보낼 께 있음을 알림) → 여기서 충돌이 나도 RTS는 작은 패킷이라 시간 손해가 없다. Data 전체를 보낸 것이 아니기 때문.
    - 와이파이 프레임
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/7f77a300-4ba5-49fe-b760-ccb299dc9542/image.png)
        
        - AP라는 디바이스는 링크레이어 디바이스(link layer device의 대표적으로는 switch-MAC addr 없음!가 있다)이다.  AP는 MAC addr가 존재한다. IP 패킷을 해석할 능력이 없기 때문에 주소를 3개 포함하여 보낸다.
        - AP의 MAC addr가 존재해야하는 이유는 무선이기 때문에 누구한테 가는지가 특정되기 않아서 필요하다.
