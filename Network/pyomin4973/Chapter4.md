- 4.2 What’s inside a router?
    - network layer: transport segment from sending to receiving host. on sending side encapsulates segments into datagrams. network layer procols in ever host, router
    - 라우터의 2가지 기능(포워딩과 라우팅)
        - 포워딩: 들어온 패킷의 목적지를 가지고 포워딩 테이블을 참고해서 entry 찾어서 그 방향으로 보낸다. 빠른 속도로 처리하는 것이 필요하다. entry의 실제 주소를 들어가면 크기가 커지기 때문에 그 range만 들어간다.(~시 ~구는 어디다. 세부정보까지 가지 않고) 가장 길게 prefix가 매칭된 것을 따라간다.
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/c068147f-8f3f-4cc1-a652-0b22a038ccf6/Untitled.png)
        
        - 라우팅: two key router functions(run 라우팅 algorthims-RIP, OSPF + forwarding datagrams from incoming to outgoing link). 라우터는 포워딩테이블 참고해서 input port에서 output port로 옮겨주는 역할을 한다. 이때 라우팅 프로세서가 포워딩 테이블 만들어줌.
            
            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/cd940ba8-0cef-44df-a517-23e9f9e31146/Untitled.png)
            
- 4.3 The Internet protocol (IP): IPv4, Addressinng
    - IP datagram format(header+{data-TCP segment가 담겨있음})
        - header 정보
            - time to live(TTL): 라우터가 포워딩시 -1씩 갱신하는 정보. 도착전까지 0이되면 이 패킷이 버려진다. 영원히 이 패킷이 살아남지 못하게, 네트워크에서 무한루프에 빠지지 않게 수명을 준다.
            - upper layer: IP에서 TCP로 올려줄 때처럼 어디로 올려줘야하는지를 명시한다. 즉 IP의 data에 담긴것이 TCP/UDP/ICMP인지에 대한 여부 등을 담길 수 있다.
            - 데이터부분에 많이 담겨서 전달될 수록 하는 것이 오버헤드가 크다. 하지만 40byte짜리도 있는데 이는 TCP의 피드백에 해당하는 것이다. data 부분없이 ACK를 위한 것. 오버헤드는 있지만 네트워크를 위해서 존재.
    - IP Address(IPv4)
        - A unique 32 bit number
        - Identifies an interface: 외부와의 인터페이스다. 인터페이스가 여러개있는 디바이스도 있는데(즉 IP주소가 여러개인 것), 라우터이다. 즉 IP주소는 호스트를 지정하는 것이 아니라 인터페이스를 지칭한다.
    - IP주소를 배정하는 방식
        - 그냥 풀에서 필요할 때마다 꺼내서 주는 방식은 scalability challenge가 있다. 매칭시키는 포워딩 테이블이 커져서 IP주소를 배정할 때 문제가 생긴다.
        - Hierarchical Addressing: IP prefixes에서 어떤 network에 속하는지에 대한 network ID와 네트워크의 어떤 호스트인지에 대한 host ID로 나눠놨다. /24라는 뜻은 24앞부분이 네트워크 ID라는 부분. (즉 24-bit prefix와 2^8 address를 가지고 있다는 뜻이다.)
        - Scalability Improved가 생긴다. 같은 네트워크에 속해있으면 네트워크 아이디가 같아진다. forwarding table이 단순해지고 매칭도 빨라진다.
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/5508c082-9249-4c40-a360-955787355d97/Untitled.png)
        
        - 이를 머신들이 이해할 수 있도록 subnet mask라는 개념이 생겼다. 어디까지가 네트워크 아이디고 어디까지가 호스트 아이디인지를 명시.
        - 네트워크 아이디의 비트수는 어떻게 결정할지. 옛날에는 Class에 따라 prefix를 결정하는 방식으로 했지만 host수가낭비되거나 부족한 경우가 많았다. 그래서 prefix를 유연하게 하는 것이 필요하여 나온 것이 CIDR이다. CIDR(Classless Inter-domain routing) 특정 기관 사이즈에 맞게 prefix 크기 결정해서 주는 방식이다. prefix크기를 작으면 호스트를 크게 지원할 수 있다.
        - prefix matching- Longest prefix match forwarding
            - 가장 길게 맞는 것과 매칭에서 나아가는 방식.
            
            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/57121761-cd8f-4ee9-bf3d-4432aefe5275/Untitled.png)
            
        - subnets: 같은 네트워크 ID를 가진 인터페이스의 집합이다. can physically reach each other without intervening router. 라우터를 거치지 않고 접근할 수 있는 인터페이스의 집합이다.
        - 라우터는 인터페이스가 여러개있는 디바이스인데, 인터페이스만큼 IP 주소를 가지는 것, 그래서 각 인터페이스의 서브넷이 다 다르다. 여러 개의 서브넷에 속해있는 중간자(교집합)이다. 그래서 다른 서브넷에 가기 위해서는 공유지인 라우터를 거쳐갈 수 밖에 없는 것이다.
        
         * 밑의 그림에서 서브넷은 6개. 각 라우터는 서브넷 3개에 속해져 있다.
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/93b722fc-8c4d-4261-804d-2f5d236cef5a/Untitled.png)
        
    - NAT(Network Address Translation)
        - **IPv4에서 IPv6로 갈아타지 못하는 이유는 라우터를 바꿔야 하는데 라우터의 소유자가 다 달라서 장비를 바꾸라고 하기에는 비용 문제가 있다. 또 생태계를 바꾸기에 쉽지 않다. IP가 부족하지만 NAT로 해결하고 있다.(주소공간 부족문제를 근본적으로 바꾸지 않고 가능)
        - 내부적으로만 유일한 주소를 배정한다. 다른 네트워크에서도 겹치는 주소를 사용가능. 그렇기 때문에 내부가 외부로 나가면 못 돌아오는 문제가 생긴다. 나갈땐, gateway의 IP주소로 바꿔줌(globally unique). 들어올때도 gateway로 들어왔다가 분배해주는 식이다.
            
            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/8bc35355-edfb-4866-af08-7bdca20fef07/Untitled.png)
            
        - host 10.0.0.1 sends datagrams to 128.119.40.196,80 → gateway에서 src 주소를 바꾼다. Nat router changes datagram source addr to 138.76.29.7,5001(translation table에 적어둠) → reply arrives dest.addres 138.76.29.7 → Nat router changes datagram dest addr to 10.0.0.1
            - IP 주소 뿐만 아니라 포트번호까지 바꾼이유는 겹치지 않는 포트번호를 사용하기 위함. 포트번호로 누군지 판단해서 reply를 보내주기 위함이다.
            - 서버입장에서는 (구글 입장에서는) 한양대 NAT를 거쳐서오면 모든 디바이스가 한양대 gateway(하나의 IP)로만 보임.
