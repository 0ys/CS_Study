- DNS domain name system
    - 프로세스와 프로세스 사이의 커뮤니케이션인데 프로세스가 다른 머신에 존재하는 경우에 그 프로세스의 주소를 적어줘야 한다. 인터넷 주소체계로 전달히기 위해서는 IP 주소와 포트 번호를 사용해서 보낸다. 서버의 포트번호는 정해져있다.(http 서버의 경우는 디폴트로 80이다.)
    - IP를 우리가 적기는 귀찮으니까 호스트 네임에 해당하는 ip주소를 기억해두는 개념이다.(이름- 전화번호를 저장하는 전화번호부처럼)
        - 호스트네임- IP주소 값 저장
        - 서버를 구현해두고 값을 저장하면 가장 간단한 형태이지만 이렇게 하면 검색시간이 엄청 커짐(record 개수는 이름개수인데 이름 개수가 거의 무제한이니까 검색시간이 늘어나는 것). 또 하나에 트래픽이 몰리면 서비스가 늦어짐. 만약 서버가 다운됐을 경우, 전세계가 브라우징 못하는 결과가 나온다.
        
    - a distributed, hierarchical database로 해놨다(분산되고 계층화로 관리가 편하고 검색속도높)
        - root name servers: 같은 copy를 가지고 있는게 전세계 13개
        - TLD(authoritative servers)
            - local DNS server→root DNS server→top-level domain servers(TLD DNS Server)→ authoritative DNS servers(난 모르는데 이거에 대한 답을 알려주는 곳을 알려줄께)
            - top-level domain servers: responsible for com, org, .. and all top-level ccountry domains. e.g., kr, jp, fr
            - authoritative DNS servers: 네트워크를 운영하는 모든 기관은 각자 자기자신의 authoritative DNS 서버를 가진다.
                - organization’s own DNS server, providing authoritative hostname to IP mappings for organization’s named host
        - Local DNS name server: does not strictly belong to hierarchy. 결과들을 캐시하고 있는 것. Local DNS에 물어보고 없으면 나가서 물어보는 시스템. 왠만하면 여기서 hit을 하는 경우가 많음
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/0e17325d-5a50-48b7-8d23-68f981e5cc55/Untitled.png)
        
    - DNS records: 실제적인 디렉토리는 필드가 4개이다.
        - NAME, VALUE, TYPE, TTL
        - type: A,NS,CNAME,MX가 옵션으로 들어간다.
            - NS: 그 도메인을 관리하는 name server의 호스트 이름을 저장하고 있다.
            - A: 호스트 이름과 Address를 저장한다(IP로)
                - NS와 A가 쌍으로 같이 다님.
            - 계층의 젤 마지막은 A타입만 가지고있다. 어디에 가서 알아봐라는 처지가 아니라서
                - 성균관 학생이 [www.hanyang.edu](http://www.hanyang.edu) → 성균관의 local name server 답변이 NS와 A가 쌍으로와서 A라는 name server한테 주소를 물어보게 된다. → 마지막 계층까지 가다가 A레코드 받아서 hanyang.edu의 IP 받으면 끝
            - 새로운 스타트업 네트워크 구성할 때 → authoritative DNS Server 구축(A타입 데이터 가짐) →그리고 위에 .com DNS 서버에 가서 NS와 A타입 2개를 적어두면 된다.
                
                ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/d2e37b65-2b8d-4460-b86c-c0084ab6b74f/Untitled.png)
                

- Socket Programming
    - socket: An interface between application and network
    - 프로세스 사이에 메시지 통신을 위한 인터페이스가 필요하다. 우체통 구멍에 편지 집어넣는것. 소캣 구멍을 통해 메세지를 집어 넣는것
    - OS 사용자 계층이 보내는 방식은 TCP/UDP → 소캣에도 2가지 종류가 있다.(TCP 소캣: socket stream, UDP 소캣: 소캣 데이터그램)
    - 소캣 create→ bind→(wait for connections)→ accept connection
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/754ef25a-cb90-451b-b4f1-b4824859d71c/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/1472719d-32af-421e-9c5a-c519575bd3fb/Untitled.png)
    
