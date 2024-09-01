1. OSI 7 layer와 각 계층
    1. physical layer: 물리적 특성을 이용해 통신 케이블로 데이터 전송
        1. 단위: bit
        2. 장비: 케이블, 리피터, 허브
    2. data link layer: MAC addr 기반으로 물리적 연결 과정에서 생기는 오류 검출, 흐름 제어 등을 수행
        1. 단위: frame
        2. 이더넷
    3. Network layer: 논리적 주소인 IP addr를 담당하며, 패킷의 전달 경로 결정
        1. 단위: packet
        2. router
    4. Transport layer: 종단 간 메시지 전송에서 오류 검출과 흐름 제어를 담당
        1. 단위: segment
        2. TCP/ UDP
    5. session layer: 양쪽 Host 간 연결을 수립/ 유지/ 종료시키는 역할
    6. presentation layer: 코드 간의 번역을 담당
    7. Application layer: 사용자에게 통신을 위한 서비스 제공. 인터페이스 역할

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/b2c91cec-27b6-4d18-87ae-abb6d8d7fbf7/image.png)

** 패킷을 잘라서 보내는 이유

많은 데이터를 한번에 보내게 되면 손실의 가능성이 있고 대역폭을 너무 많이 차지하게 된다. 패킷의 흐름을 원활히 조절하기 위해 잘라서 보냄

- TCP/ IP 프로토콜과 각 계층
    - 인터넷에서 표준으로 사용되고 있는 네트워크 프로토콜
    - 특징: 점대점(두 노드간의 통신), 전이중(양방향 통신이 가능), 흐름 제어(수신 측의 처리량을 고려하여 데이터 전송), 혼잡 제어(특정 네트워크 구간에 데이터가 몰리지 않도록 처리)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/a376f179-d117-447b-b5ed-1f0d33d51c0b/image.png)
    
    - TCP의 hand-shaking
        - 핸드셰이크란, 호스트 간 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/94415713-a9ac-47a6-ab40-f5bcf863da74/image.png)
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/60ae33e9-a664-4bb0-b005-34102616a371/image.png)
        

- UDP
    - 실제 데이터 단위를 받기 위해 IP를 사용
    - 여러 컴퓨터를 거치지 않고 데이터를 주고받을 컴퓨터끼리 직접 연결시 사용
    - 정보를 받는 컴퓨터는 포트를 열어두고, 패킷이 올때까지 기다리며 데이터가 오면 모두 다 받아드림. → 패킷이 도착했을 때 출발지에 대한 정보(IP와 PORT)를 알 수 있다.
        - 비신뢰적, 안정적X, 속도가 매우 빠르고 편해서 데이터 유실이 일어나도 큰 상관이 없는 스트리밍, 화면 전송에 사용
- TCP
    - 신뢰적인 데이터 전달 기능
        - 흐름제어, 순서번호, 확인 응답, 타이머 등의 기술 사용
        - 프로세스에게 데이터가 순서대로 정확히 전달되도록함
    - 혼잡제어
        - 보내는(송신쪽)의 트래픽을 조절하여 스위치/ 링크의 혼잡을 방지
        - 혼잡한 네트워크 링크에서 각 TCP 연결이 링크의 대역폭을 공평하게 공유하여 통과하게 함
    - UDP는 속도증가와 지연감소를 위해서 사용
    - TCP는 신뢰성이 중요한 경우 사용(몇몇의 정보도 손실되면 안되는 경우)
- UDP와 TCP의 공통점과 차이점
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/a17f33b3-35c9-4073-a6ec-f97e04835ed3/image.png)
    
    - UDP segment
        - 포트번호: 목적지 호스트가 정확한 프로세스에게 애플리케이션데이터를 넘기게 한다.
        - 체크섬: 세그먼트에 오류가 발생했는지 검사하기 위해 사용.
        - 길이: 헤더를 포함하는 UDP 세그먼트의 길이를 나타냄
    - TCP segment
        - 포트번호: IP정보와 결합하여 출발지, 도착지 구분위해 사용
        - Sequence Number: SYN 패킷을 보낼 때, 동기화를 위해 사용되는 번호
        - ACK Number: ACK패킷을 보낼 때 동기화를 위해 사용하는 번호
    
- 흐름제어의 개념
    - 종단 시스템간 통신에서 패킷의 프름을 제어하는 것
    - Stop and wait: 매번 전송한 패킷에 대한 응답을 받아야 다음 패킷을 보내주는 방식
    - Sliding window: 수신 측에서 설정한 윈도우 크기만큼 송신 측에서 확인 응답 없이 세그먼트를 전송할 수 있게 한다.
        - 데이터 흐름을 동적으로 조절하여 제어하는 기법

- HTTP 프로토콜
    - HTTP란 데이터를 주고받기 위한 프로토콜. 서버/ 클라이언트 모델을 따름
    - HTTP는 애플리케이션 레벨의 프로토콜로 TCP/ IP 위에서 작동
    - 특성: stateless(상태 정보를 저장하지 않음). connectionless(클라이언트의 요청에 맞는 응답을 보낸 후 연결을 끊음)
        - 장점: 통신 간의 연결상태 처리나 상태 정보를 관리할 필요X→ 서버 디자인 간단 (각 HTTP 요청에 독립적으로 응답만 보내주면 됨)
        - 단점: 과거 통신정보를 몰라서 인증 매번 필요 → 쿠키나 세션 사용으로 데이터 처리
    - HTTP와 HTTPS의 차이점
        - HTTP(TCP→HTTP): 평문 데이터를 전송하는 프로토콜. 중요 정보 주고받을 시 제 3자에 의해 조회 → 보안 취약
        - HTTPS(TCP→SSL→HTTP): HTTP에 암호화가 추가된 프로토콜. 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 공개키 암호화를 지원. → 속도가 느림. 인증서 발급 및 유지 위한 추가 비용 발생
        
- SSL(Secure Socket Layer)
    - 인터넷을 통해 전달되는 정보를 보호하기 위해 개발한 통신 규약
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/b0ea6868-2017-4f95-b2ca-c6cb92299e37/image.png)
    

- 대칭키 암호화, 비대칭키 암호화
    - 대칭키와 비대칭키는 양방향 암호화 방식
    - 대칭키: 암호화와 복호화에 같은 암호키를 쓴다. → 누군가 암호키를 가로채면 암호화된 정보 유출 위험
    - 비대칭키: 암호화와 복호화시 키를 서로 다른 키로 사용 (개인키- 타인 노출 불가, 공개키- 공개적으로 개방되어 있음)
- DNS(Domain Name Server)
    - 네트워크 통신에 사용되는 IP주소는 사람이 이해하기 어렵다
    - 이를 위해 각 IP에 부여한 이름이 Domain
    - DNS: 숫자로 이루어진 IP주소와 일정한 형식을 가진 도메인을 서로 매핑시키는 정보를 가지고 있다. 도메인에 연결된 서버의 IP주소를 찾아주는 역할.
    - 주소창에 도메인 입력시 호스트(통신을 주고받는 주체)는 해당 도메인이 연결된 DNS로 가서 서버 IP 요청 → 요청받은 네임서버가 해당 도메인과 연결된 서버 IP찾아서 알려줌
        - 보통 local cache에서 hit 되는 경우에 컴퓨터가 해당 도메인의 IP를 기억하고 있어서 그걸 사용→ 찾지못하면 DNS 검색
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/dcc27151-ba27-4e47-809b-946895d3db2f/image.png)
    

- HTTP Method와 REST
    - HTTP 메소드는 클라이언트가 서버에게 사용자 요청의 목적을 알리는 수단(GET, POST, PUT, PATCH-일부 데이터 변경, DELETE)
    - REST(Restpresentional State Transfer)
        - url로 자원을 명시하고 HTTP 메서드를 통해 해당 자원에 대한 CRUD 연산을 적용하는 것 의미
        - 자원: 데이터베이스의 정보. 클라이언트가 DB에 접속해 변경하는 것은 위험하므로 REST API 사용
        - 클라이언트가 서버에 데이터를 CRUD하겠다고 HTTP 메서드로 요청시 서버는 로직에 따라 DB에 접근하여 요청 처리
    - RESTful 은 REST 아키텍처로 구현된 웹 서비스. → REST API를 제공하는 웹서비스는 RESTful하다.
- 쿠키와 세션
    - 쿠키: 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일
        - 사용자 인증이 유효한 시간을 명시 가능
        - 유효 시간 동안 브라우저가 종료되어도 인증이 유지된다.
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/75accf06-ba22-4f42-95ee-d7ae5a0b321e/image.png)
        
    - 세션: 쿠키 기반, but 사용자 정보를 브라우저에 저장하기 않고 서버측에서 관리한다.
        - 서버에서는 클라이언트를 구분하기 위해 세션 ID를 부여하며 웹 브라우저가 서버에 접속해서 브라우저를 종료할 때까지 인증 상태를 유지
        - 사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지
            
            → 동접자 수가 많은 웹 사이트인 경우 서버에 과부하 →성능저하
            
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/ba9e41a1-7c34-4545-be4a-9abf98d4b73d/image.png)
        
    - 쿠기와 세션 차이점
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/d56bc969-c6f4-4e58-a38c-ba64f8aacfcf/image.png)
    

- CORS(Cross-Origin Resource Sharing)
    - 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
    - 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송 지원

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/51e44aa0-810c-43e8-beb2-c55ab3dc43bf/image.png)

- IPv4와 IPv6의 차이
    - IP(인터넷 프로토콜): 호스트 간 패킷 교환 네트워크에서 패킷 혹은 데이터그램으로 불리는 정보를 주고 받는데 사용하는 프로토콜
    - IPv4는 헤더에 option이 존재하고 단편화와 재조립 기능을 제공해서 큰 데이터 그램을 쪼개 전송하고 도착지에서 재조립
    - IPv6는 빠른 속도를 위해 단편화 및 재조립 기능 제공X . 데이터 그램의 우선순위를 설정할 수 있는 priority 비트가 존재한다
- 서브네팅, 서브넷 마스크
    - 서브넷 마스크: IP 주소의 효율적 사용을 통해 낭비를 막기 위해 네트워크 아이디와 호스트 아이디를 구별하는 구분자
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/fd4d7a3a-98b2-4055-aa73-9cde21a3207b/image.png)
        
    - IP와 서브네팅
        - IP라는 한정적 자원 활용하기 위해, 노드에 주소를 효율적으로 할당하는 것이 중요.
        - 서브네팅: IP를 쪼개서 네트워크 파트+호스트 파트로 구성한다. IP 주소에 따라 5개의 클래스로 구분되어 각 클래스에 따라 네트워크 파트와 호스트 파트 정해짐.
    - 서브넷 마스크
        - 효율적 주소관리를 위해 내부적으로 호스트 파트를 새로운 네트워크 파트와 호스트 파트로 나누어 사용
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/ce89bb3c-8a43-428b-a1ca-cf0cfde5fa1a/image.png)
        

- MAC주소
    - Data link layer에서 통신을 위해 네트워크 인터페이스에 할당한 식별자.
    - 모든 네트워크 장비는 자신의 MAC 주소가 있으며 주소는 장비 제조업체가 할당 → MAC 주소는 물리적 주소
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/10b074be-f328-44d4-8646-5e1e82d02095/image.png)
    

- 라우터, 스위치, 허브의 차이(LAN)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/deccc8e9-047f-496b-b83d-5fa84b390f33/image.png)
    

- 이더넷
    - 근거리 유선통신을 위해 사용. CSMA/CD 프로토콜 사용
    - 장점: 적은 용량의 데이터를 보낼 때 성능이 좋다. 비용이 적고 관리가 쉽다. 구조가 단순하다.
    - 단점: 충돌발생으로 인한 지연이 생길 수 있다.

- 라우팅 프로토콜
    - 패킷을 전달할 때 어느 경로로 갈지 정하는 것
    - 라우팅 경로 고정여부에 따라 정적라우팅, 동적라우팅으로 구분
    - 동적라우팅에서 AS를 기준으로 내부적으로 동작하면 내부라우팅(RIP, OSPF)과 외부라우팅(BGP, EGP)
    - 라우팅 테이블 관리(동적라우팅)
        - distance vector- 벨만포드 알고리즘: 현재위치까지의 방향과 거리를 기록한 라우팅 테이블을 인접한 라우터들에게 전달과 갱신.
            - 메모리가 적게 들고 구성이 쉽지만 전체 테이블 구성시간 길어짐. 같은 경로를 반복해서 도는 루핑 문제
        - link state-다익스트라 알고리즘: 인접테이블에 정보를 전달했으며 또 그 인접 테이블들은 이 정보를 바로 인접 테이블로 넘겨, 직접 연결되지 않은 모든 라우터들도 현재 정보 파악 가능
            - 정확하고 루핑문제 없다 →대형 네트워크에서 많이 사용
            - 메모리 소모와 CPU 로드가 많음
- 공인IP와 사설 IP의 차이
    - **공인 IP**
        - 전세계에서 유일한 IP로 ISP(인터넷 서비스 공급자)가 제공하는 IP주소
        - 외부에 공개되어 있기 때문에 인터넷에 연결된 다른 장비로부터 접근이 가능하다.
        - 그에 따라 방화벽 등과 같은 보안 설정을 해주어야 한다.
    - **사설 IP**
        - 어떤 네트워크 안에서 사용되는 IP주소
        - IPV4의 부족으로 인해 모든 네트워크가 공인 IP를 사용하는 것이 불가능하기 때문에 네트워크 안에서 라우터를 통해 할당받는 가상의 주소이다.
        - 별도의 설정 없이는 외부에서 접근이 불가능하다.
- SMTP
    - MTP(Simple Mail Transfer Protocol)은 인터넷에서 이메일을 보내기 위해 사용하는 TCP/ IP 프로토콜
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/28b92b1a-4689-4aad-9b89-4b3901afc203/image.png)
    
- 데이터 캡슐화와 역캡슐화
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/98b11392-12e1-443c-ba03-3320859d5154/image.png)
    
- 소캣
    - Application 프로세스와 종단간 통신을 제공하는 transport 프로토콜 사이의 인터페이스.
    - WebSocket:  서버와 브라우저 간 연결을 유지한 상태로 데이터를 교환할 수 있도록 하는 프로토콜
        - 브라우저 간 서버 간 양방향 메시지 송수신 규칙
        - 깜박임 없이 필요한 부분만 다시 그리는 상호작용 방식 가능하게
    - [socket.io](http://socket.io): 서버와 브라우저의 양방향 통신을 가능하게 하는 모듈
- delay, timing, throughput의 개념(네트워크 상 성능)
    - delay: 하나의 데이터 패킷이 출발 지점에서 도착 지점에 도착한 시간 의미
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/bd727b0d-9d4e-4096-a9ed-db6c0da1dea5/image.png)
        
    - timing: delay의 변동(변화량)을 의미
        - 같은 스위치가 아닌 경우, 패킷마다 대기 시간이 달라지기 때문에 생김
    - throughtput: 지정된 시간 동안 실제로 전송된 정보량을 의미한다.
- 네트워크 topology
    - 컴퓨터끼리 정보를 교환하고 교류하는 형태를 의미하는 네트워크에서 토폴로지는 **컴퓨터들의 특정한 망구성 방식**을 의미한다.
    - star: 중앙에 위치한 메인 노드를 통해 다른 노드와 소통할 수 있는 구조
        - 장점: 장애 발견이 쉽고 관리가 용이
        - 단점: 메인 노드에 장애가 발생하면 전체 네트워크 사용 불가능
    - bus: 공통배선을 통해 노드들이 연결되어 있어서, 한노드의 신호가 모든 노드에 전달된다.
        - 장점: 노드 추가 및 삭제 용이. 한 노드에 장애가 발생해도 다른 노드에 영향을 주지 않음
        - 단점: 공통 배선의 크기(대역폭)이 제한되어 있으므로 배선에 과부하가 걸릴 경우 네트워크 성능 저하
    - Ring: 각 노드가 양 옆으로 연결된 원형 구조, 단방향으로 신호 전달
        - 장점: 단방향 구조로 단순하고, 중간에 있는 노드들이 증폭기 역할(거리 제약 적어짐)
        - 단점: 노드 추가 및 삭제 어렵
    - Mesh: 다수의 노드가 서로 연결된 형태
        - 장점: 노드의 장애에 여향받지 않으며 유연한 대체가 가능하고 안정적
        - 단점: 구축 비용이 크고, 노드 추가에도 비용이 많이 듦.

- ARP
    - IP주소로 MAC주소를 얻어오기 위한 프로토콜이 ARP이다
    - 이더넷 프레임의 구성요소 중 type field에는 IP 패킷인지 ARP query인지를 명시함. ARP query에는 궁금해하는 interface의 IP주소(e.g., 1.1.1.1)이 담김.
    - IP주소에 해당하는 것만 ARP query에 반응한다. ARP response를 담아서 A한테 알려주게 된다. A는 알게된 정보를 ARP table에 작성한다
    
- 패킷교환/회선교환을 비교/설명해주세요.
    
     Packet Switching
    
    네트워크 응용에서 엔드시스템들은 서로 메시지를 교환한다. 긴 메시지들은 작은 packet들로 쪼개진다. 출발지에서 도착지까지 각 패킷은 커뮤니케이션 링크와 패킷스위치로 흘러간다.
    
    store-and forward, forwarding table과 라우팅 알고리즘
    
     Circuit Switching
    
    서킷 스위치는 소통을 위해 제공되는 resources들은 종단간 커뮤니케이션 세션의 기간 동안 예약된다. 패킷 스위치는 이러한 자원이 예약되지 않습니다.
    
    multiplexing(time/ frequent)
    
    회로 교환 방식은 수요와 관계없이 전송 링크의 사용을 미리 할당하며, 할당되었지만 필요하지 않은 링크 시간은 사용되지 않습니다. 반면에, 패킷 교환 방식은 수요에 따라 링크 사용을 할당합니다.
