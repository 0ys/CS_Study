# 1.1 What is the internet

인터넷이 어떤 것인지 두가지로 설명할 수 있는데 첫째는 볼트와 너트이고 둘째는 분산된 applications에 대한 서비스를 제공하는 네트워킹 infrastructure라는 관점이다.

## 1.1.1 볼트와 너트 설명

인터넷은 컴퓨팅 디바이스들을 상호연결하는 컴퓨터 네트워크이다.

옛날에는 데스트탑 PC가 이런 컴퓨팅 디바이스에 속했지만 최근 노트북이나 TV 등도 인터넷에 연결되고 있다. 이후 컴퓨터 네트워크는 시대에 뒤쳐진 용어처럼 보인다.

이렇듯 늘어나고 있는 모든 디바이스들은 host나 end system으로 불린다. end system은 communication link나 packet switches의 network로 연결되어 있다. 여러 링크들은 데이터를 서로다른 속도로 전송하는데, 링크의 전송 속도는 bits/second이다. 패킷이라고 불리는 정보의 결과 패키지는 end system 으로 보내지고 그곳에서 원본 데이터로 합쳐진다. 패킷 스위치 중 대표적인 것은 라우터나 link-layer switches이다.

communication link나 패킷 스위치의 sequence는 네트워크의 rout나 path로 end system으로 전달된다.

end system은 주로 Internet Service ProviderS(ISPs)를 통해 인터넷에 접근한다. 각 ISP는 그 자체로 패킷 스위치와 통신 링크로 이루어진 네트워크이다.(?) ISP는 end system의 네트워크 접근에 대한 여러 유형을 제공한다. ISP는 content provider의 인터넷 접근을 제공한다.

end system, 패킷 스위치 등은 인터넷 안에서 정보를 주고받는 것을 컨트롤하는 protocol을 작동지킨다. Transmission Control Protocol(TCP)와 Internet Protocol(IP)는 가장 중요한 프로토콜이다. IP protocol은 패킷의 포맷을 명시한다. 

모든 사람들이 각 프로토콜이 하는 것에 동의하는 것이 중요. 그래서 인터넷 스탠다드가 나왔는데 IETF 2016에 의해 개발됨. IETF standard는 requests for comments(RFCs)로 불림. RFCs는 TCP IP같은 프로토콜을 정의함.

## 1.1.2 A services Description

중요 단원만 하자!

분산된 application에 서비스를 제공하는 infrastructure가 인터넷이다.

온라인 소셜미디어와 같은 응용들을 분산된 application이라고 한다. 이유는 그것들이, 서로 데이터를 교환하는 다수의 end system을 포함하고 있기 때문이다.

인터넷에 붙어있는 end system들은 프로그램이 어떻게 데이터를 전달하라고 인터넷 infrastructure에 물어보는지가 명시되어 있는 소캣 인터페이스를 제공한다. 이런 소캣 인터페이스는 전달하는 프로그램이 무조건 따라야할 룰이 집합이다.

## 1.1.3 What is a Protocol?

 네트워크 프로토콜은 휴먼 프로토콜과 비슷하다. 2개 이상의 소통하는 remote entity들을 포함하는 인터넷의 활동들은 프로토콜에 의해 지배된다. 예를들어 라우터들 속 프로토콜은 출발지에서 도착지까지 패킷의 path를 결정한다.

프로토콜은 두 개 이상의 소통하는 entity들 사이에 교환되는 메시지의 포맷과 순서를 정의한다. + 메시지의 전송이나 수신때에 이뤄지는 actions들도 정의

컴퓨터 네크워킹의 field를 마스터하는 것은 네트워킹 프로토콜을 이해하는 것과 같다

# 1.2 The Network Edge

End system은 호스트라고도 불림.  그 이유는 그들은 web 브라우져 같은 응용 프로그램을 host하기 때문이다. 호스트는 cilent(노트북 등)와 서버(비디오 저장 등) 두 개의 카테고리로 갈림. 대부분의 서버들은 큰 데이터 센터에 있다.

## 1.2.1 Access Networks

Home Access: DSL, Cable, FTTH, and 5G Fixed Wireless

가정용 브로드밴드 접속의 두 가지 가장 널리 퍼진 유형은 digital subscriber line(DSL)과 케이블이다. 가정은 보통 같은 로컬의 전화 company에게서 DSL internet access을 얻는다. DSL이 사용될 때 사용자의 전화 company는 그것의 ISP이기도 하다. 이런 가정용 전화선은 데이터와 전통적 전화 신호를 동시에 들고간다. 이때 각각은 다른 주파수로 암호화되어 있다. DSL 기준은 다수의 전송속도를 정의하는데 downstream과 upstream 속도느 다르다. 두 속도가 다르기 때문에 이런 access는 비대칭이라고 불린다.

DSL가 전화 회사의 기존 local 전화 infra를 사용할때, cable Internet access는 케이블 티비 회사의 존재하는 케이블 티비 인프라를 사용한다. 가정들은 케이블 인터넷 access를 케이블 tv를 제공하는 같은 회사를 통해 얻는다. 케이블 인터넷 access는 공유된 브로드캐스트 medium이다. 특히 head에서 보내진 모든 패킷들은 downstream을 따라 모든 집로 링크되어 있다. 이 이유로 많은 사용자가 동시에 downstream 채널에서비디오를 다운받는다면 실제 속도는 상당히 낮아진다.(?)

이것보다 더 빠른 스피드를 가지는 것은 fiber to the home(FTTH)다. 이것은 CO를 직접 집으로 최적의 fiber path를 통해 제공한다. 또 5G fixed wireless가 나왔는데, 가정용 엑세스에 높은 속도 뿐만아니라 설치에 대한 비용 문제를 없앴다.

Access in the Enterprise(and the Home): Ethernet and Wifi.

대학 캠퍼스에선 LAN(local area network)가 edge 라우터와 end system을 연결하는데 사용된다. twisted-pair copper선을로 연결하는 LAN 중 Ethernet이 가장 널리 사용된다. 무선 LAN setting의 경우에는 유저가 패킷을 access point로 보내면 기업의 네트워크(유선 이더넷)에 연결된다. 유선 이더넷은 곧 유선 인터넷으로 연결된다.

IEEE 802.11에 기반한 무선 LAN 엑세스는 wifi로 잘 알려져 있다.

## 1.2.2 Physical Media

비트는 physical medium을 따라 최적의 펄스나 전자기적 웨이브를 통해 전파되며 전송된다. physical media는 2개의 카테고리 guided media(twisted-pair copper wire, 재료가 아닌 인건비 문제)와 unguided media(공기)로 나누어짐.

- twisted-pair copper wire: 가장 싸고 흔하게 사용됨. UTP(Unshielded twisted pair)가 컴퓨터 네트워크를 통해 사용된다.
- coaxial cable: guided shared medium으로써 사용됨
- Fiber Optics: 빛의 펄스를 conduct하는 얇은 flexible medium이다.
- Terrestrial Radio Channels: 전자기적 스펙틀럼에서 신호를 전달한다.
- Satellite Radio Channels: 두 유형의 위성이 소통에 이용됨. (geostationary satellites, low-earth orbiting(LEO) satellites)

# 1.3 The Network core

링크와 스위치의 네트워크를 통해 데이를 옮기는 근본적인 2개의 접근은 서킷 스위칭과 패킷 스위칭이다.

## 1.3.1 Packet Switching

네트워크 응용에서 엔드시스템들은 서로 메시지를 교환한다. 긴 메시지들은 작은 packet들로 쪼개진다. 출발지에서 도착지까지 각 패킷은 커뮤니케이션 링크와 패킷스위치로 흘러간다.

Store-and Forward Transmission

대부분의 패킷 스위치는 링크로의 input시에 store-and-forward 전송을 사용한다. 패킷 스위치가 패킷의 첫 번째 비트를 아웃바운드 링크로 전송하기 시작하기 전에 패킷 전체를 받아야 함을 의미합니다.

Lbit를 각각의 속도가 R인 N 링크로 구성된 path에서 출발지에서 목적지까지 1개의 패킷을 보낼 때 end-to-end delay는 다음과 같다.

d(end-to-end)=N*(L/R)

Queuing Delays and Packet Loss

각 패킷 스위치는 여러 링크에 연결되어 있습니다. 각 연결된 링크마다 패킷 스위치는 출력 버퍼(출력 큐라고도 함)를 가지고 있으며, 이 버퍼는 라우터가 해당 링크로 보내려고 하는 패킷을 저장합니다.

또 store-and-forward delay에서 패킷은 output buffer queuing delays를 겪는다. 이런 지연은 다양하고 네트워크의 혼잡 수준에 따라 다릅니다. 버퍼는 유한하기때문에 버퍼가 다 차면 패킷 loss가 생긴다. 막 도착한 패킷이나 이미 큐에 있던 패킷 중에 탈락한다.

Forwarding Tables and Routing Protocols

인터넷에서 모든 엔드 시스템은 IP address라고  불리는 주소를 가지고 있다. 패킷의 헤더에 이런 도착지 정보가 포함되어 있다. 더 구체적으로는 각 라우터는 도착지 주소로 갈 수 있는 (라우터의 아웃바운드 링크로의) map해주는 forwading table이 있다. 라우터가 포워딩 테이블을 통해 얻은 패킷의 도착지 주소를 사용하고 적절한 outbound link로 연결한다.

## 1.3.2 Circuit Switching

서킷 스위치는 소통을 위해 제공되는 resources들은 종단간 커뮤니케이션 세션의 기간 동안 예약된다. 패킷 스위치는 이러한 자원이 예약되지 않습니다.

네트워크가 서킷을 만들때, 연결동안 네트워크의 링크에서 constant 전송 속도를 예약한다. 보장된 속도로 갈 수 있다. 두 호스트가 소통하고자할때 네트워크는 두 호스트 사이의 end-to-end connection을 만든다.

Multiplexing in circuit-switched networks(Figure 1.14)

링크안 서킷은 frequenct-division multiplexing(FDM)이나 time-division multiplexting(TDM)을 사용한다. FDM에서는 주파수 스펙트럼이 나뉘어 진다. TDM에서는 시간이 고정된 기간의 frame으로 나뉘어진다. 그리고 각 프레임은 고정된 개수만큼의 time slot으로 나뉘어진다.

패킷 교환 방식의 지지자들은 항상 회로 교환 방식이 비효율적이라고 주장해왔는데, 이는 전용 회로가 침묵 기간 동안 silent periods 상태에 있기 때문입니다.

Packet Switching versus circuit switching

패킷 교환 방식의 지지자들은 (1) 패킷 교환 방식이 회로 교환 방식보다 전송 용량을 더 잘 공유할 수 있으며 (2) 회로 교환 방식보다 구현이 더 간단하고 효율적이며 비용이 적게 든다고 주장합니다. 회로 교환 방식은 수요와 관계없이 전송 링크의 사용을 미리 할당하며, 할당되었지만 필요하지 않은 링크 시간은 사용되지 않습니다. 반면에, 패킷 교환 방식은 수요에 따라 링크 사용을 할당합니다.

최근 트랜드는 패킷 스위칭을 사용한다

## 1.3.3 A Network of Networks

access ISP는 무선이나 유선으로 제공된다. 엔드 유저와 컨텐츠 제공자들을 access ISP로 연결하기는 어렵다. 그러므로 ISP들끼리 상호연결되어있어야 한다. 이것은 네트워크의 네트워크로 진행된다. 접속 ISP가 글로벌 전송 ISP에게 비용을 지불하기 때문에, 접속 ISP는 고객이라고 하고 글로벌 전송 ISP는 제공자라고 합니다. 몇몇 회사들이 global transit ISP를 만드는데 이익을 위해 그들 자신만의 global transit ISP를 build한다.

특정 지역에서 regional가 있어서 지역 연결에 사용한다. 각 regional ISP는 tier-1 ISP(가상의 global transit ISP와 비슷)에 연결된다.

Pop(points of presence)은 **아래 레벨(access ISP)**을 제외하고 모든 레벨의 계층에 존재. Pop은 provider(제공자)의 ISP에 있는 라우터들의 집합이다.  tier-1 ISP를 제외한 어떤 ISP든 mult-home을 선택할 수 있는데 2개 이상의 제공자ISP에 연결하는 것이다.

비용을 줄이기 위해서 가까이에 있고 계층의 같은 레벨에 있는 것들은 peer를 할 수 있는데 그들은 같이 네트워크에 즉시 연결될 수 있다. 그래서 그들 사이의 모든 트래픽이 직접 연결을 통해 업스트림 중개자를 거치지 않고 통과합니다.

구글같은 content-provider networks는 여러 데이터 센터가 있고 각 센터에 100개 이상의 서버가 있다.

# 1.4 Delay, Loss, and Throughput in Packet-Switched Networks

## 1.4.1 Overview of Delay in Packet-Switched Networks

패킷은 한 노드(호스트나 라우터)에서 다음 노드로 이동하면서 delay들을 만난다. nodal processing delay, queuing delay, transmission delay, propation delay가 있는데 이런 delay 들이 축적되어 total nodal delay를 만들어낸다. 인터넷 애플리케이션들의 성능에 네트워크 지연이 영향을 끼친다.

### Processing Delay

패킷의 헤더를 검사하고 패킷을 어디로 전달할지 결정하는 데 필요한 시간

패킷의 비트가 업스트림 노드에서 라우터 A로 전송되는 동안 발생한 비트 수준 오류를 확인하는 데 필요한 시간

### Queuing Delay

패킷이 링크로 전송되기를 기다리는 시간. 특정 패킷의 대기 지연 시간은 링크로 전송되기 위해 큐에 대기하고 있는 이전에 도착한 패킷의 수에 따라 달라집니다.

### Transmission Delay

패킷의 길이가 L이고 링크의 전송속도가 R bits/sec라면 전송 지연 시간은 L/R입니다. 이는 패킷의 모든 비트를 링크로 밀어 넣는 데 필요한 시간입니다.

### Propagation Delay

비트가 링크에 밀려 들어가면, 라우터 B로 전파되어야 합니다. 링크의 시작점에서 라우터 B까지 전파되는 데 시간이 필요하다. 이 지연속도는 링크의 물ㄹ리적 medium에 따라 결정된다.

## 1.4.2  Queuing Delay and Packet Loss

a이 패킷이 큐에 도착하는 평균 속도라고 하고 R이 전송속도라 하자. 여기서 모든 패킷은 L개의 비트로 이루어져 있다. 이때 La/R은 traffic intensity라고 불리는데 queuing delay를 추정할 때 중요한 역할을 한다.

La/R>1일 때, 만약 La/R > 1이면, 비트가 큐에 도착하는 평균 속도가 큐에서 비트가 전송될 수 있는 속도를 초과합니다. 이런 불행한 상황에서는 큐가 끝없이 증가하는 경향이 있으며, 대기 지연 시간은 무한대로 가까워질 것입니다. → 1 초과로 가지 않도록 하는 것이 필요하다

이제 La/R ≤ 1인 경우를 고려해봅시다. 이 상황에서는 도착하는 트래픽의 특성이 대기 지연에 영향을 미칩니다. 예를 들어, 패킷이 주기적으로 도착한다면, 즉 패킷이 L/R 초마다 하나씩 도착한다면, 모든 패킷은 빈 큐에 도착하게 되므로 대기 지연이 발생하지 않습니다. 반면에, 패킷이 주기적으로 도착하지만 일시에 몰려 도착하는 경우에는 평균 대기 지연이 상당할 수 있습니다. 예를 들어, N개의 패킷이 동시에 매 (L/R)N 초마다 도착한다고 가정해봅시다. 그러면 첫 번째로 전송되는 패킷은 대기 지연이 없지만, 두 번째로 전송되는 패킷은 L/R 초의 대기 지연이 발생하며, 일반적으로 n번째로 전송되는 패킷은 (n-1)L/R 초의 대기 지연이 발생합니다.

### Packet Loss

패킷이 꽉 찬 큐에 도착하게 되면, 일런 패킷을 저장할 장소가 없기 때문에 라우터는 패킷을 drop하게 되고 그 패킷은 lost 상태가 된다. 이런 overflow는 traffic intensity가 1 초과일 때 나타난다.

## 1.4.3  End-to-End Delay

source부터 destination까지의 total delay는 다음과 같다. 이때 출발지 host와 도착지 host 사이에는 N-1개의 라우터가 있다.

d(end-end)=N( d(proc)+ d(trans)+ d(prop))

## 1.4.4 Throughput in Computer Networks

순간의 instantaneous throughput(처리량)은 호스트 B가 파일을 수신하는 속도(비트/초)이다.

파일이 F 비트로 구성되어 있고 호스트 B가 모든 F 비트를 수신하는 데 T 초가 걸린다면, 파일 전송의 average throughput은 F/T 비트/초입니다.

# 1.5 Protocol Layers and Their Service Models

## 1.5.1 Layered Architecture

### Protocol Layering

하드웨어와 소프트웨어 네트워크는 layer에서 프로토콜을 실행한다. 각 프로토콜은 레이어 안에 속해있는데, (service model of a layer)레이어에게 제공하는 서비스들에 대해 알아본다. Protocol layering는 개념적 및 구조적 이점이 있습니다 [RFC 3439]. 우리가 본 것처럼, layering는 시스템 구성 요소를 논의하는 구조적인 방법을 제공합니다. 모듈화는 시스템 구성 요소를 업데이트하기 쉽게 만듭니다.

다양한 layer의 프로토콜은 프로토콜 스택이라고 불린다. (Application-Transport-Network-Link-Physical)

### Application Layer

application layer에는 network applications와 그들의 application-layer protocols이 있다. HTTP 프로토콜, SMTP 프로토콜, FTP 프로토콜 등이 포함되어있다. domain name system(DNS)와 같은 응용 프로토콜의 도움으로 인간 친화적인 인터넷 end system에 대한 번역 function도 있다. 

다른 종단의 application과 정보의 패킷을 교환하는 프로토콜을 사용한다. application layer의 정보 packet을 message라고 부른다.

### Transport Layer

application과 endpoints 사이에서 application layer의 message를 전송한다. TCP와 UDP라는 2가지 전송 프로토콜이 있다. TCP는  connection-oriented service를 제공하는데 네트워크가 혼잡할때 전송속도를 조절하는 것처럼, 보장된 전송을 하는 프로토콜이다. UDP는 connectionless 서비스를 제공한다. 

transport layer 패킷을 segment라고 부른다.

### Network Layer

하나의 로스트에서 다른 곳으로 network layer의 패킷(데이터그램)을 옮기는 역할을 한다. 출발지 호스트의 인터넷 전송 계층 프로토콜(TCP 또는 UDP)은 전송 계층 세그먼트와 목적지 주소를 네트워크 계층에 전달합니다. 이는 마치 우편 서비스에 목적지 주소가 적힌 편지를 맡기는 것과 같습니다. 네트워크 계층은 그런 다음 목적지 호스트의 전송 계층에 세그먼트를 전달하는 서비스를 제공합니다.

### Link Layer

네트워크 계층은 데이터그램을 링크 계층으로 전달하고, 링크 계층은 해당 경로를 따라 다음 노드로 데이터그램을 전달합니다. 이 다음 노드에서 링크 계층은 데이터그램을 다시 네트워크 계층으로 전달합니다.

링크 계층에서 제공하는 서비스는 링크에서 사용되는 특정 링크 계층 프로토콜에 따라 다릅니다. 네트워크 계층은 각각의 다른 링크 계층 프로토콜로부터 서로 다른 서비스를 받게 됩니다. 이 책에서는 링크 계층 패킷을 프레임이라고 부를 것입니다

### Physical Layer

링크 계층의 역할은 전체 프레임을 하나의 네트워크 요소에서 인접한 네트워크 요소로 이동시키는 것이었다면, 물리 계층의 역할은 프레임 내의 개별 비트를 한 노드에서 다음 노드로 이동시키는 것입니다.

## 1.5.2 Encapsulation

데이터는 end system의 protocol stack을 up and down 하면서 전달된다. 라우터나 link-layer switches는 프로토콜 스택의 전체 층을 실행하지는 않지만 host는 모든 5개 계층을 실행한다.(?아마)

전송  host에서 application-layer message는 transport layer로 전달된다. 그후 더 추가적 정보가 붙어서transport-layer segment 형태 → network-layer datagram → link-layer frame로 재생성되어 도착지로 전송된다.

# 1.6 Networks Under Attack

The Bad Guys Can Put Malware into Your Host Via the Internet

malware는 디바이스에 들어와서 감염할 수 있다. 파일 삭제나 spyware를 설치해서 비밀키 등을 빼갈 수 있다. 흔한 malware는 self-replicating이다.

한 번 감염된 호스트에서, 그 호스트는 인터넷을 통해 다른 호스트로 침입하려고 시도하며, 새로 감염된 호스트에서도 다시 다른 호스트로 침입하려고 합니다. 이런 방식으로 자기 복제하는 악성 소프트웨어는 기하급수적으로 빠르게 확산될 수 있습니다.

### The Bad Guys Can Attack Servers and Network Infrastructure

보안 위협으로는 denial-of—service(Dos)가 있다. DoS 공격은 네트워크, 호스트 또는 기타 인프라를 정당한 사용자들이 사용할 수 없게 만듭니다.

분산 서비스 거부(DDoS) 공격에서는 공격자가 여러 출처를 제어하고, 각 출처가 대상에 대해 트래픽을 집중적으로 전송합니다. DDoS 공격은 단일 호스트로부터의 DoS 공격보다 탐지하고 방어하기 훨씬 어렵습니다.

### The Bad Guys Can Sniff Packets

모든 패킷의 복사본을 기록하는 수동 수신 장치를 패킷 스니퍼라고 합니다. 스니퍼는 유선 환경에서도 배치될 수 있습니다. 패킷 스니퍼는 수동적이기 때문에, 즉 채널에 패킷을 주입하지 않기 때문에 탐지하기 어렵습니다.

### The Bad Guys Can Masquerade as Someone You Trust

인터넷에 가짜 출발지 주소로 패킷을 주입할 수 있는 능력을 IP 스푸핑이라고 하며, 이는 한 사용자가 다른 사용자로 가장할 수 있는 여러 방법 중 하나에 불과합니다.

이 문제를 해결하기 위해서는 엔드포인트 인증이 필요합니다. 즉, 메시지가 우리가 생각하는 출처에서 실제로 시작되었는지를 확실히 확인할 수 있는 메커니즘이 필요합니다.
