- UDP
    - connectionless transport
    - segment header: header field가 4개(source port, dest port, length, checksum, application data(payload)). checksum은 에러가 났는지 확인하는 부분이다. header는 mux/demux 사용, 유실 되긴 하지만 엉뚱한 데이터가 전송되는 것은 막는다.
    - no connection establishment(which can add delay)
    - simple: no connection state at sender, receiver
    - small header size
    - no congestion control: UDP can blast away as fast as desired

- 3.5 TCP
    - 인터넷의 전송 계층이다 connection-oriented,reliable transport protocol.
    - 3.5.1 tcp connection
        - connection-oriented: application이 데이터를 보내기 시작하기 전에 두 프로세스는 서로 handshake를 해야한다.
        - Full-duplex service 제공: 한 호스트의 process A가 다른 호스트의 process B로 application 데이터를 flow할때 B도 A로 동시에 보낼 수 있다.
        - Point to point이다. Single sender와 single receiver 사이의 connection이다. 반면 multicasting은  한 sender가 많은 receiver에게 데이터를 전송한다.
    - 3.5.2 TCP segment structure
        - tcp segment의 헤더 구조:  헤더는 source와 도착지 포트 정보를 포함하고 있다. 헤더는 checksum field도 포함하고 있다. 32 bit sequence number field, 32bit acknowledgement number field는 reliable data transfer serive에서 사용한다. Receive window는 flow-control에서 사용된다. Header length field는 tcp 헤더의 길이를 명시하는데 사용된다. Option field는 송수신자가 최대 segment size를 협의할 때 사용된다. Flag field는 6bit를 가지는데, ack비트는 acknowledgement  field에서 carried된 값이 합당한지 확인할 때 사용한다.
    - 3.5.3 round-trip time estimation and timeout
        - tcp는 lost segment를 회복하기 위해 timeout/retransmit 메커니즘을 사용한다.
    - 3.5.4 reliable data transfer
        - tcp는 reliable data transfer service를 만들어낸다. Tcp는 프로세스가 TCP 수신 버퍼에서 읽어내는 데이터 스트림이 손상되지 않고, 간격이 없으며, 중복되지 않고, 순서대로 이루어지도록 보장합니다. 즉, 바이트 스트림은 다른 사이드의 연결에서 종단에 의해 전송된 바이트 스트림과 동일하다.
        - Timeout triggered 재전송의 문제점은 timeout 주기가 상대적으로 길 수 있다는 점이다. 그 이유는, 세그먼트가 없어졌을 때 이 긴 timeout period는 잃어버린 패킷의 재전송을 sender가 지연하도록 하기 때문이다.
            - 다행히도 sender는 패킷 로스를 timeout event전에 알아차리기도 한다. 그 이유는 duplicate Ack때문인데,  중복 ACK는 송신자가 이미 이전에 ACK를 받은 세그먼트를 다시 ACK하는 것을 의미합니다. 이는 일반적으로 수신 측에서 패킷이 손실되었거나 지연되었음을 나타내는 신호로 사용됩니다. 이러한 중복 ACK를 통해 송신자는 패킷 손실을 감지하고 손실된 세그먼트를 재전송할 수 있습니다.
        - TCP fast retransmit
            - time out period often relatively long: long delay before resending lost packet
            - detect lost segments via duplicate ACKs.
                - sender often sends many segments back to back
                - if segment is lost, there will likely be many duplicate ACKs
            - if sender receives 3 ACKs for same data(triple duplicate ACKs)
                
                ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/463860de-4ef4-4b30-841b-240f364c7199/Untitled.png)
                
    
    - 3.5.5 Flow Control
        - TCP는 송신자가 수신자의 버퍼를 넘치는 상황을 방지하기 위해 흐름 제어 서비스를 제공합니다. 흐름 제어는 송신 속도와 수신 애플리케이션이 읽는 속도를 일치시키는 속도 조정 서비스입니다.
        - TCP는 흐름 제어를 위해 수신 창(receive window)이라는 변수를 유지합니다. 간단히 말해, 수신 창은 송신자에게 수신자의 여유 버퍼 공간이 얼마나 있는지에 대한 정보를 제공합니다.
        - TCP의 헤더에 있는 receive window에 여유공간을 담아서 피드백을 보내는 형식이다.
            
            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/e1ec6414-32b3-4be0-b138-8d70c1c45734/Untitled.png)
            
    

- TCP congest control
    - congestion: 네트워크가 처리할 수 있는 데이터보다 더 많은 데이터가 들어왔을 때 생기는 현상
        - informally too many sources sending to much data too fast for network to handle
        - 라우터에서 패킷 유실이 일어날 수 있다.
    - 네트워크 상황을 report 받을 수 있는 시스템이 필요하다
        - ack가 잘 오면 네트워크가 잘 있는지 추측, 피드백을 통해서
        - condition window를 additive increase(천천히 늘리고) + multiplicative decrease(1/2로 줄인다)
            - send buffer의 window size가 한꺼번에 데이터를 보낼 수 있는 양. flow-control과 congest-control (condition window) 중 작은 값을 보내서 overflow 안나게 함.
            - segment 크기는 클 수록 좋다 → maximum segment size는 default다. condition window크기가 MSS에 따라 늘어나거나 줄어듦. 피드백이 잘오면 condition window가 늘어나는 식이다.
            - 늘어나다보면 네트워크에 문제가 생기고 피드백이 안온다 → 그 때는 condition window사이즈를 절반으로 줄이고 linear increase 또 시작됨.
        - 제일 처음으로 보낼때 condition window사이즈를 어떤 식으로 잡을 것이냐.
            - TCP Slow Start: when connection begins, increase rate exponentially until first loss event.
                - initially cwnd= 1MSS
                - double cwnd every RTT
                - done by incrementing cwnd for every ACK received
            - initial rate is slow but ramps up exponentially fast
            - time expire나 3 dup ACK가 왔을 때는 loss되었다고 판단하고 1/2로 cwnd을 줄인다.
