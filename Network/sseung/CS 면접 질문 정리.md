### 1. OSI 7 layer와 각 계층에 대해 설명해주세요.

1. **`Physical layer`**: 물리적 특성을 이용해 통신 케이블로 데이터를 전송
   1. 단위: bit
   2. 장비: 케이블, 리피터, 허브
2. **`Data Link layer`**: MAC address 기반으로 물리적 연결 과정에서 생기는 오류 검출, 흐름 제어 등을 수행.
   1. 단위: frame
   2. ex: 이더넷
3. **`Network layer`**: 논리적 주소인 IP address를 담당하며, 패킷의 전달 경로를 결정
   1. 단위: Packet
   2. ex: 라우터
4. **`Transport layer`**: End to End간 메시지 전송에서 오류 검출과 흐름 제어를 담당
   1. 단위: Segment
   2. ex: TCP, UDP
5. **`Session layer`**: 양쪽 Host 간 연결을 수립/유지/종료시키는 역할
6. **`Presentation layer`**: 코드 간의 번역을 담당
7. **`Application layer`**: 사용자에게 통신을 위한 서비스 제공, 인터페이스 역할

### 1-1. Frame, Packet, Segment, Datagram을 비교해주세요.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/capsulation.png

- **`Packet`** : 컴퓨터 간에 데이터를 주고받을 때, 네트워크를 통해 전송되는 **데이터 조각**
  - 송신 측(애플리케이션)은 많은 양의 데이터를 한번에 보내는 것이 아니라, 일정 단위로 잘라서 보낸다. 각 계층에서 필요한 정보는 캡슐화/역캡슐화되어 전달되고, 수신 측은 받은 패킷을 다시 조립해서 사용한다.
- **`Segment`** : 전송 계층에서 신뢰할 수 있는 통신을 구현하기 위한 헤더를 데이터에 붙이는데, 이렇게 만들어진 패킷을 세그먼트라고 부른다.
- **`Datagram`** : 네트워크 계층에서 다른 네트워크와 통신하기 위한 헤더를 세그먼트에 붙인것을 데이터그램이라고 부른다.
- **`Frame`** : 데이터 링크 계층에서 물리적인 통신 채널을 열기 위해 패킷에 헤더와 트레일러를 붙인다. 트레일러는 데이터를 전달할 때 데이터 끝 부분에 붙이는 정보로, 주로 에러 검출에 사용된다.

> **왜 패킷을 잘라서 보낼까?**

많은 데이터를 한번에 보내게 되면, 데이터 손실의 가능성이 있으며, 대역폭(신호를 전송할 수 있는 주파수 범위)을 너무 많이 차지하게 되므로, 패킷의 흐름을 원활히 조절하기 위함이다.

### 2. TCP/IP 프로토콜과 각 계층에 대해 설명해주세요.

TCP/IP는 인터넷에서 표준으로 사용되고 있는 네트워크 프로토콜을 의미한다.

TCP/IP는 IP를 중심으로 한 여러 프로토콜의 집합체로, TCP/IP 5계층 혹은 TCP/IP 4계층(링크계층과 물리계층을 하나의 계층으로 보는 경우)으로 불린다.

- **`네트워크 인터페이스 계층`**
  - IP 패킷의 물리적인 전달을 담당하는 서브네팅 기능을 제공하며 dial-up 회선, LAN 등이 해당된다.
- **`인터넷 계층`**
  - 비연결형 서비스 즉, 데이터그램 방식으로 호스트 사이에 IP 패킷을 전달하는 기능과 라우팅 등을 수행한다.
- **`트랜스포트 계층`**
  - 호스트 사이의 종점간 연결을 제공하고 종점간의 데이터 전달을 처리한다.
- **`응용 계층`**
  - TCP/IP 프로토콜을 이용하는 응용 서비스로서 TCP 또는 UDP가 지원하는 응용으로 각각 구분할 수 있다.

### 3. OSI 7계층과 TCP/IP 계층의 차이를 설명해주세요.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/2a5ec66e-dc1a-465b-9313-fea64f52a827/image.png)

!https://user-images.githubusercontent.com/36303777/96871341-1e965b00-14ad-11eb-8d65-d2329cff8d3c.png

### 4. TCP의 특징을 말해보세요.

- **`점대점`** : 두 노드간의 통신
- **`전이중`** : 양방향 통신이 가능
- **`흐름 제어`** : 수신측의 처리량을 고려하여 데이터를 전송
- **`혼잡 제어`** : 특정 네트워크 구간에 데이터가 몰리지 않도록 처리

### 5. TCP의 3way hand shaking와 4 way hand shaking를 비교해 설명하세요.

**핸드셰이크**(Handshake)란, 호스트 간 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

### 3-way handshake

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/3-way-handshake.png

**`3-way handshake`**는 TCP의 연결을 초기화 할 때 사용한다. 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기전에 한쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다. 양쪽 모두 상대편에 대한 초기 순차일련변호를 얻을 수 있도록 한다. 절차는 다음과 같다.

1. 접속 요청 클라이언트가 연결 요청 메시지 전송한다.**`(SYN)`**
2. 접속 요청을 받은 서버가 요청을 수락한다는 확인 메시지를 보낸다. **`(ACK)`**
3. 동시에 접속 요청을 받은 서버도 접속 요청을 한 클라이언트에 연결 요청을 보낸다.

   **`(SYN) → (SYN + ACK)`**

4. 마지막으로 접속 요청 클라이언트가 수락 확인을 보내 연결을 맺는다.**`(ACK)`**

> **💡 단순히 응답을 주고받는데 2-way Handshake가 아닌 3-way 인 이유?**

TCP/IP 통신은 양방향성 통신이다. 위의 그림의 1번 과정에서 클라이언트가 연결 요청을 SYN으로 보내면, 서버는 클라이언트가 요청한 SYN에 대한 대답(ACK)과 함께, 자신도 연결하겠다는 요청의 의미로 SYN을 보내고, 클라이언트로부터 요청에 대한 대답(과정 3)을 받아야한다. 따라서, 2-way handshaked에서는 성립될 수 없다.

### 4-way handshake

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/4-way-handshake.png

**`4-way handshake`**는 세션을 종료하기 위해 수행되는 절차이다.

1. 클라이언트가 연결을 종료하겠다는 **`FIN`** 플래그를 전송한다.
2. 서버는 일단 확인메시지(ACK)를 보내고 자신의 통신이 끝날때까지 기다리는데, 이 상태가 **`CLOSE_WAIT`** 상태이다.
3. 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 **`FIN`** 플래그를 전송한다.
4. 클라이언트는 확인했다는 메시지를 보낸다.

> **💡 용어**

- **`SYN(Synchronization)`**: 연결요청, 세션을 설정하는데 사용되며 초기에 시퀀스 번호를 보낸다.
- **`ACK(Acknowledgement)`**: 보낸 시퀀스 번호에 TCP 계층에서의 길이 또는 양을 더한 것과 같은 값을 ACK에 포함하여 전송한다.
- **`FIN(Finish)`** : 세션을 종료시키는데 사용되며 더 이상 보낸 데이터가 없음을 표시한다.

### 5-1. TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계) 단계가 차이나는 이유가 무엇인가요?

연결 설정 과정과 다르게, 연결 종료 과정에서 고려해야 하는 경우가 존재하는데, 이는 전송중인 데이터에 대한 경우이다. 클라이언트는 아직 서버로부터 못 받은 데이터가 있을 것을 대비하여 일정시간동안 세션을 남긴다(`TIME_WAIT`). 모든 데이터를 다 보내서 더 이상 보낼 데이터가 없다는 의미의 `FIN`을 받으면, 바로 연결을 종료한다.

### 5-2. 만약 Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하면 어떻게 될까요?

클라이언트에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 drop되고 **데이터는 유실**될 것이다.

클라이언트는 이러한 현상에 대비하여 서버로부터 **`FIN`**을 수신하더라도 일정시간 동안 세션을 남겨놓고, 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 **`TIME_WAIT`** 라고 한다.

일정시간이 지나면, 세션을 만료하고 연결을 종료시키며, **`CLOSE`** 상태로 변화한다.

### 5-3. 초기 Sequence Number인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유가 무엇인가요?

연결할 때 사용하는 포트는 유한범위 내에서 사용하고 시간이 지남에 따라 재사용된다. 따라서 두 통신 호스트가 과거에 사용된 포트번호 쌍을 사용하는 가능성이 존재한다.

서버 측에서는 패킷의 **`SYN`**을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 number가 전송된다면 **이전의 연결로 부터 오는 패킷으로 인식할 수 있다.**

이러한 문제가 발생할 가능성을 줄이기 위해서 난수로 ISN을 설정하는 것이다.

### 6. **UDP란 무엇인가요?**

사용자 데이터그램 프로토콜은 비연결형 전송계층 프로토콜이다.

UDP는 **비신뢰적인 서비스**로서, 프로세스에 의해서 전송된 데이터가 손상되지 않은채로 목적지에 도착하는 것을 보장하지 않는다. 또한 **비연결형 서비스**이며, 오류검출은 선택사항이다.

**[UDP의 특징]**

- UDP는 흐름제어, 오류제어 또는 손상된 세그먼트의 수신에 대한 재전송 X
  - 내용이 전송 중에 손실 될 수 있고, 전송되는 세그먼트의 순서가 바뀔 수 있음
- 수신자와 송신자 간의 handshaking X
- 흐름제어를 하지 않기 때문에 전송 속도가 빠름 **(실시간)**
  - 신뢰성보다 전송 속도가 중요한 부문에서 사용
  - EX) 유튜브와 같은 스트리밍 어플리케이션
- 멀티캐스트/ 브로드캐스트 가능 (IPTV)

### 7. UDP와 TCP의 공통점과 차이점을 말해보세요.

### 공통점

1. **트랜스포트 다중화/역다중화 기능**: **`호스트 대 호스트 전달`**을 **`프로세스 대 프로세스 전달`**로 확장
2. **무결성 검사(오류검출)**: 헤더에 오류 검출 필드를 포함

### 차이점

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/3b78073e-11e7-4c7f-904c-cf4c24bdd5f6/image.png)

**`UDP`**는 **비신뢰적인 서비스**로서, 프로세스에 의해서 전송된 데이터가 손상되지 않은채로 목적지에 도착하는 것을 보장하지 않는다. 또한 **비연결형 서비스**이며, 오류 검출은 선택사항이다.

UDP는 비연결형 서비스이므로 연결 설정이 불필요하고 연결 상태가 없다. 따라서 연결을 설정하기위한 어떠한 지연이 없고, 유지해야하는 정보가 없기 때문에 더 많은 클라이언트를 수용할 수 있다.

또한 UDP의 패킷 오버헤드가 TCP에 비해 더 작다는 장점이 있다. 그러나 혼잡제어를 사용하지 않아, 네트워크가 폭주 상태에 빠지는 것을 막을 수 없다는 단점과 신뢰적이지 않으므로, 몇몇의 정보를 잃어버릴 수 있다는 단점이 존재한다.

**`TCP`**는 가장 기본적인 **두가지 기능도 제공하면서, 신뢰적인 데이터 전달 기능, 연결지향형 서비스, 혼잡 제어 등의 기능을 제공한다.**

**신뢰적인 데이터 전달**은 흐름제어, 순서번호, 확인응답(ACK), 타이머 등의 기술을 사용하여 프로세스에게 데이터가 순서대로 정확히 전달되도록 하는 역할을 한다. 종단 시스템 간에 IP의 비신뢰적인 서비스를 프로세스 사이의 신뢰적인 데이터 전송 서비스로 만들 수 있으며, TCP에서의 오류 검출은 필수사항이다.

**혼잡 제어**는 송신 측의 트래픽을 조절하여 스위치/링크의 혼잡을 방지하는 역할을 한다. 이는 특정 애플리케이션을 위해 제공하는 특정 서비스가 아니라, 전체를 위한 서비스로서, 혼잡한 네트워크 링크에서 각 TCP 연결이 링크의 대역폭을 공평하게 공유하여 통과하도록 해준다.

따라서, **UDP**는 **속도 증가**와 **지연 감소**를 위해서 많이 사용되고, **TCP**는 **신뢰성**이 중요한 경우에 사용된다.

### 7-1. TCP와 UDP의 헤더를 비교해주세요.

**UDP segment**의 간략한 구조는 아래와 같다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/udp-segment.png

**UDP 헤더**는 2바이트씩 구성된 4개의 필드를 가진다. UDP 헤더는 `출발지 포트번호`, `목적지 포트번호`, `체크섬`, `길이`로 이루어져있다.

- **포트번호:** (목적지)호스트가 정확한 프로세스에게 애플리케이션 데이터를 넘기게 하기위해 사용
- **체크섬:** 세그먼트에 오류가 발생했는지를 검사하기 위해 사용
  - UDP 헤더와 데이터를 모두 포함하여 체크
- **길이:** 헤더를 포함하는 UDP 세그먼트의 길이(UDP헤더와 데이터를 합친 길이)를 나타냄

---

**TCP segment**의 간략한 구조는 아래와 같다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/b0aba84a-ea01-40bf-8039-a86dcccc2da3/image.png)

다른 출발지 주소를 가지는 세그먼트는, 다른 소켓을 통해서 프로세스에 전달된다.

UDP와 다르게, TCP 세그먼트는 출발지 주소가 다르면, 다른 소켓으로 전달된다.

- **포트번호**는 IP 정보와 결합하여 출발지, 도착지를 구분하기 위해 사용된다.
- **Sequence Number:** SYN 패킷을 보낼 때, 동기화를 위해 사용되는 번호이다. 초기 Sequence Number를 ISN이라 부르며, 여기에는 랜덤한 수가 담긴다.
- **Ack Number:** ACK 패킷을 보낼 때 동기화를 위해 사용되는 번호

### 8. 흐름 제어의 개념과 대표적인 방식을 설명해주세요.

흐름 제어란 종단 시스템간 통신에서 패킷의 흐름(속도)을 제어하는 것을 의미한다.

- **Stop and wait 방식:** 전송한 패킷에 대한 응답을 받아야 다음 패킷을 보내주는 방식이다.
- **Sliding window 방식:** 수신 측에서 설정한 윈도우 크기만큼 송신 측에서 확인 응답 없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하여 제어하는 기법이다.
  https://t1.daumcdn.net/cfile/tistory/253F7E485715ED5F27

### 9. HTTP 프로토콜에 대해 설명해주세요.

HTTP(Hyper Text Transfer Protocol)이란 HTML 문서와 같은 데이터를 주고 받기 위한 프로토콜이며, 서버/클라이언트 모델을 따른다. HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 동작한다.

HTTP는 Method, Path, Version, Headers, Body 등으로 구성된다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/8aa43ba6-3f22-4f49-879a-f0cc3d08c2e7/image.png)

HTTP는 상태 정보를 저장하지 않는 **Stateless**의 특징과 클라이언트의 요청에 맞는 응답을 보낸 후 연결을 끊는 **Connectionless**의 특징을 가지고 있습니다.

- **장점**
  - 통신 간의 연결상태 처리나 상태정보를 관리할 필요가 없어 서버 디자인이 간단하다.
  - 각각의 HTTP 요청에 독립적으로 응답만 보내주면 된다.
- **단점**
  - 이전 통신의 정보를 모르기 때문에 매번 인증을 해줘야 한다.
    → 해결 방안 : 쿠키나 세션을 사용해서 데이터를 처리한다.

### 10. HTTP와 HTTPS의 차이점은 무엇인가요?

- HTTP 동작 순서 : TCP → HTTP
- HTTPS 동작 순서 : TCP → **SSL** → HTTP

**`HTTP`**는 평문 데이터를 전송하는 프로토콜이기 때문에, HTTP로 중요한 정보를 주고 받으면 제 3자에 의해 조회될 수 있다.

**`HTTPS`**는 **HTTP에 데이터 암호화가 추가된 프로토콜**이다. HTTPS는 네트워크 상에서 중간에 제 3자가 정보를 볼 수 없도록 공개키 암호화를 지원하고 있다.

HTTP는 암호화가 추가되지 않았기 때문에 **보안**에 취약한 반면, HTTPS는 안전하게 데이터를 주고받을 수 있다. 하지만 HTTPS를 이용하면 암호화/복호화의 과정이 필요하기 때문에 HTTP보다 속도가 느리다. 또한 HTTPS는 인증서를 발급하고 유지하기 위한 추가 비용이 발생하다.

개인 정보와 같은 민감한 데이터를 주고받아야 한다면 HTTPS를 이용해야 하지만, 단순한 정보 조회 등 만을 처리하고 있다면 HTTP를 이용한다.

HTTP는 원래 TCP와 직접 통신했지만, HTTPS에서 HTTP는 SSL과 통신하고 SSL이 TCP와 통신함으로써 암호화와 증명서, 안전성 보호를 이용할 수 있게 된다.

### 11. SSL의 개념과 통신 과정에 대해 설명해보세요.

**Secure Socket Layer**로 인터넷을 통해 전달되는 정보를 보호하기 위해 개발한 통신 규약이다.

HTTPS는 HTTP에 SSL과 같은 보안 계층을 제공한다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/59529e72-8d29-4c00-95a4-82ddb8ef8c7b/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/9c0c8216-9b4a-43f8-b5a8-dfcd88ccefd0/image.png)

1. 클라이언트에서 서버에 Client Hello 메시지를 보냄
   1. 전송 정보: 클라이언트에서 가능한 TLS 버전, 세션 식별자, 암호 설정 등
2. 클라이언트의 메시지를 받은 서버는 SeverHello 메시지를 클라이언트에게 보냄
   1. 전송 정보
      1. ClientHello 메시지 정보 중 서버에서 사용하기로 선택한 TLS 버전, 세션 식별자, 암호 설정 등
      2. 서버의 인증서(별도의 인증 기관(CA)에서 발급한 것) (공개키) → 서버의 신뢰성 인증
3. 클라이언트는 서버에서 받은 인증서 검증 → 임의의 pre-master secret을 생성 (대칭키 후보)
4. 서버가 보낸 인증서에 포함된 공개키를 사용해 암호화 → 서버에 전송
5. 서버는 전송받은 정보를 자신의 비밀키로 복호화 → pre-master secret을 알아냄
6. 이 정보를 사용해 master secret을 생성 → master secret에서 세션키 생성
   - **서버와 클라이언트는 동일한 세션키를 가짐**
7. 세션키를 활용한 대칭키 암호화 방식 통신
8. 세션 종료 → 세션키 폐기

### 12. 대칭키, 비대칭키 암호화 방식에 대해 설명해주세요.

**[대칭키]**

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-1.png

- 암호화와 복호화에 **같은** 암호키를 사용하는 암호화 방식
- **장점**
  - 공개키에 비해 암호화 및 복호화가 빠름
- **단점**
  - 암호화 통신을 하는 사용자끼리 같은 대칭키를 공유해야함
  - 사용자가 증가할수록 관리할 키가 많아짐
  - 대칭키를 전달하는 과정에서 해킹의 위험이 있음
- 해결 방법
  - 공개키 암호화 방식
- 대표 알고리즘: DES, 3DES, AES, SEED, ARIA

---

**[비대칭키]**

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-2.png

- 암호화와 복호화에 사용하는 암호키가 서로 **다른** 암호화 방식
  - 송신자: 수신자의 공개키를 이용하여 메시지를 암호화
  - 수신자: 자신만이 갖고 있는 개인키를 이용해 복호화
- 장점
  - 공개키로 암호화한 메시지는 수신자의 개인키로만 해독할 수 있으므로 안전하게 메시지가 전달됨
- 단점
  - 암복호화가 복잡하고 느림
- 대표 알고리즘: Diffie-Hellman, RSA, DSA, ECC

### 13. HTTP 요청/ 응답 헤더의 구조를 설명해주세요.

### 14. HTTP와 HTTPS 동작 과정을 비교해주세요.

**[HTTP 통신 과정]**

- 서버/클라이언트 모델을 따름

> 클라이언트 -> 요청 -> 서버 -> 응답 -> 클라이언트

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-3.png

1. 클라이언트가 원하는 서버에 접속
2. 클라이언트가 서버에 요청
3. 서버가 요청에 따른 응답 결과를 다시 클라이언트에 응답
4. 응답이 끝나고 나면 서버와 클라이언트의 연결은 끊김

---

**[HTTPS 통신 흐름]**

HTTPS에는 **대칭키** 암호화와 **비대칭키** 암호화가 모두 사용됩니다. 비대칭키 암/복호화는 비용이 매우 크기 때문에 서버와 클라이언트가 주고받는 모든 메세지를 비대칭키로 암호화하면 오버헤드가 발생할 수 있습니다. 그래서 서버와 클라이언트가 최초 1회로 서로 대칭키를 공유하기 위한 과정에서 비대칭키 암호화를 사용하고, 이후에 메세지를 주고 받을 때에는 대칭키 암호화를 사용합니다.

공개키로 암호화된 메세지는 개인키를 가지고 있어야만 복호화가 가능하기 때문에, 서버(기업)을 제외한 누구도 원본 데이터를 얻을 수 없습니다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/58f7d152-b504-48ee-a414-4af4857f5fd1/a8d35ce4-308c-4115-9e36-ec2806ad1c4d.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/531ede35-60f2-4e26-9367-62a74f16f975/0f57a283-3e92-4be1-ac97-675b5911f8f7.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/4d9605f7-2aac-42f7-adcd-12e241f02b5e/d500c19e-36cc-43d7-bf2e-5b17f47955e9.png)

1. 서버는 공개키, 개인키를 만들고 인증기관(CA)에 자신의 정보와 공개키 관리 계약을 맺음
2. 인증기관은 인증기관의 개인키로 사이트에서 제출한 정보(서버 공개키, 공개키 암호화 방법)를 암호화하여 인증서를 만들어 서버에 제공
3. 사용자가 사이트에 접속하면 서버는 자신의 인증서를 웹 브라우저(클라이언트)에게 제공
4. 웹 브라우저는 인증기관의 공개키(이미 알고있음)로 인증서를 해독하여 검증 -> 사이트 정보와 서버의 공개키를 얻음
5. 얻은 서버의 공개키로 대칭키를 암호화하여 다시 서버에 보냄
6. 서버는 암호화된 대칭키를 자신의 개인키로 복호화 하여 클라이언트와 동일한 대칭키 획득
7. 이 후부터는 전달 받은 대칭키로 데이터를 주고 받음
8. 세션이 종료되면 대칭키는 폐기됨

### 15. www.naver.com에 접속했을 때, 요청을 보내고 받는 과정을 설명하세요.

**[ 웹 동작 방식 ]**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/a18c0391-9ed3-4a67-bda6-4fe7935624a7/image.png)

1. 사용자가 브라우저에 URL을 입력
2. 브라우저는 DNS를 통해 서버의 진짜 주소를 찾음
3. HTTP 프로토콜을 사용하여 HTTP 요청 메세지를 생성함
4. TCP/IP 연결을 통해 HTTP요청이 서버로 전송됨
5. 서버는 HTTP 프로토콜을 활용해 HTTP 응답 메세지를 생성함
6. TCP/IP 연결을 통해 요청한 컴퓨터로 전송
7. 도착한 HTTP 응답 메세지는 웹페이지 데이터로 변환되고, 웹 브라우저에 의해 출력되어 사용자가 볼 수 있게 됨

### 15-1. DNS는 무엇인가요?

**[DNS(Domain Name System)]**

!https://private-user-images.githubusercontent.com/81477543/250540086-41582d11-e505-4f62-bd5c-6d91a58025b6.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjQ5MDA3ODMsIm5iZiI6MTcyNDkwMDQ4MywicGF0aCI6Ii84MTQ3NzU0My8yNTA1NDAwODYtNDE1ODJkMTEtZTUwNS00ZjYyLWJkNWMtNmQ5MWE1ODAyNWI2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDA4MjklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwODI5VDAzMDEyM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdiNzEwNzI2ZTRiZWQwZGJiOTE0NTdkNTgwNWQ4ZjU0MzM2ZmQ4MDZmMTg1N2ZhNzljMWM5N2NjMWQ3OTQ0NzgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.9WfyeqYX_64Bzep3H23V_092ErTZQZSL5WcIU2ru95g

- 문자로 된 도메인 네임을 컴퓨터가 이해할 수 있는 IP 주소로 변환하는 **분산** 데이터베이스
- 응용 계층에 해당함
- UDP 방식 사용
  - 연결을 위한 준비 동작과정에 TCP를 사용하기에는 비용이 큼
  - DNS message는 40byte로 크기가 작아서 유실될 가능성이 적음

**[DNS의 구조]**

!https://private-user-images.githubusercontent.com/81477543/250541462-96dfe524-eff5-41b9-b309-506f01422dc8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjQ5MDA3ODMsIm5iZiI6MTcyNDkwMDQ4MywicGF0aCI6Ii84MTQ3NzU0My8yNTA1NDE0NjItOTZkZmU1MjQtZWZmNS00MWI5LWIzMDktNTA2ZjAxNDIyZGM4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDA4MjklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwODI5VDAzMDEyM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWY1MGU4NzUxZDE4NmEyOWZlNzhlYTc5NWY2ODFmMTg5OWE1MmQ2YmZkNGU2NjZkNjBlNTAzMDkwNDRjMmVlZDEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.xqwOHeEEgUljK9hhxBVZZ2MgsqE85g8dXW9CGrrCiWM

> **브라우저가 도메인에 해당하는 IP를 찾는 순서**

1. local cache 안에 검색한 해당 도메인의 IP가 있는지 확인 → 이미 해당 도메인을 방문한 적이 있다면 컴퓨터가 해당 도메인의 IP를 기억하고 있으므로 그것을 사용한다.
2. 만약 캐시에 없다면 컴퓨터 내부에 파일 형태로 존재하는 hosts 파일을 검색 → 해당 hosts 파일에 특정 도메인과 IP를 매핑 시켜놓으면 해당 도메인은 지정한 IP로 이동한다.
3. 만약 위의 경우에서 도메인에 대한 IP를 찾지 못하면 최종적으로 DNS를 검색한다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/dns.png

### 16. HTTP Method와 각각이 사용되는 경우에 대해서 설명해주세요.

HTTP 메소드는 클라이언트가 서버에게 사용자 요청의 목적을 알리는 '수단'이다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/e197c208-a26f-40a0-8c66-29292c632d47/image.png)

### 17. HTTP GET과 POST를 비교/ 설명해주세요.

**`GET`**은 데이터를 조회하기 위해 사용되는 방식으로 데이터를 헤더에 추가하여 전송하는 방식이다. URL에 데이터가 노출되므로 보안적으로 중요한 데이터를 포함해서는 안된다.

**`POST`**는 데이터를 추가 또는 수정하기 위해 사용되는 방식으로 데이터를 **바디**에 추가하여 전송하는 방식이다. URL에 데이터가 노출되지 않아 GET 보다는 안전하다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/da234bf9-e2cf-44be-bc8c-7733685e7c5a/image.png)

### 18. REST와 RESTful의 개념을 설명하고 차이를 말해주세요.

**`REST`**란 **Re**presentational **S**tate **T**ransfer의 약자로, URI로 웹에 존재하는 모든 자원(이미지, 동영상, DB 등)을 명시하고 HTTP 메서드를 통해 해당 자원에 대한 CRUD(Create, Read, Update, Delete) 연산을 적용하는 것을 의미한다.

→ 서버와 클라이어트 사이가 명확히 분리된다.

**`RESTful`**

- REST API의 설계 규칙을 올바르게 지키도록 설계된 시스템
- RMM의 2단계까지 만족하도록 설계된 경우

> **RESTful 하지 못한 경우**

- CRUD 기능을 모두 POST로만 처리하는 API
- 경로에 resource, id 외의 정보가 들어가는 경우 (/students/updateName)

### 18-1. URL과 URI의 의미와 차이점을 설명하세요.

> **URL 이란?**

- URL은 Uniform Resource Locator, 네트워크 상에서 통합 자원(리소스)의 “**위치**”를 나타내기 위한 규약이다. 즉, 자원 식별자와 위치를 동시에 보여준다.
  - ex) 웹 사이트 주소 + 컴퓨터 네트워크 상의 자원
- 특정 웹 페이지의 주소에 접속하기 위해서는 웹 사이트의 주소뿐만 아니라 프로토콜(https, http 등)을 함께 알아야 접속이 가능한데, 이들을 모두 나타내는 것이 URL이다.

> **URI 란?**

- URI는 Uniform Resource Identifier의 약자로, 자원을 식별자로 취급하여 나타내는 주소를 말한다.

> **URI 와 URI의 차이점**

- URI= 식별자, URL=식별자+위치

**01 | URL은 일종의 URI이다.**

https://lh6.googleusercontent.com/2dC-UX4G66CKAuXJuN0JIYmwo7rWdV8cxhOXllbn75D1zNcPqZjgjdusnFpSfuZRaY3cWUzZCZne7TRVhONhXnDiD8OLkGpQIxnu7N35P-20o6I8onKmc2mju_i3HdAK7vtjATNGdUPKlsoFoIMTFwDXUTCJShY9GwsnFgzkgPYPPK8rVJJgU-toMbilow

**02 | URL은 프로토콜과 결합한 형태이다.**

https://www.elancer.co.kr > URL

즉, 어떻게 위치를 찾고 도달할 수 있는지까지 포함되어야 하기 때문에

URL은 프로토콜 + 이름(또는 번호)의 형태

### [URI URL 구조]

https://lh4.googleusercontent.com/K9t30Sjp6cIbsLg67B-amTH927yS3q06E68DvSLK_4t364b38otQLLibFbyj_I0JH6fLB8tp5zEgVObcaSj810X1Xs2XWuwxD-_ibK8JtfsUaGgm5JNVhUhfjcH3vairIchwhKfviglEmKYYk5aH4cc74ncEaW6N9fRS5VZtKS4EGmvGSYIUSLvx04r0xQ

### 19. 쿠키(Cookie)와 세션(Session)을 설명/ 비교해주세요.

<aside>
💡 **HTTP 프로토콜의 약점(Stateless : 상태정보 유지 불가)을 보완하기 위한 개념**

</aside>

**[쿠키(Cookie)]**

- 클라이언트 로컬에 저장되어 있는 키와 값이 들어있는 파일이다
- 이름, 값, 유효시간, 경로 등을 포함하며 클라이언트의 상태 정보를 브라우저에 저장하여 참조
- EX) 자동 로그인, 아이디 저장

**[동작 방식]**

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-12.png

1. 웹 브라우저가 서버에 페이지 요청
2. 웹 서버가 상태를 유지하고 싶은 값을 쿠키로 생성
3. 서버가 응답할 때 HTTP 헤더에 쿠키를 포함해 전송 (Set-Cookie: key=value)
4. 전달 받은 쿠키를 웹 브라우저에서 관리하고 있다가 다음 요청 때 쿠키를 HTTP 헤더에 넣어서 전송

---

**[세션(Session)]**

- 일정 시간 동안 같은 브라우저로부터 들어오는 요청을 하나의 상태로 보고 그 상태를 유지하는 기술
- **서버에 접속한 이후부터 브라우저를 종료**할 때까지 유지되는 상태
- EX) 로그인 유지 (웹 페이지 내에서 화면 이동하더라도 로그인 풀리지 않음)

**[동작 방식]**

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-13.png

1. 웹 브라우저가 서버에 페이지 요청
2. 서버가 응답할 때 쿠키에 session id를 담아서 전송
3. 웹 브라우저는 브라우저를 닫기 전까지 요청할 때 전달받은 session id를 담은 쿠키를 HTTP 헤더에 넣어서 전송
4. 서버는 session id를 확인해 해당 세션에 관련된 정보를 확인한 후 응답

---

**[쿠키 VS 세션]**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/d8539768-2390-4bb4-acc3-8800162abf67/image.png)

- **사용자의 정보가 저장되는 위치**
  - 쿠키는 서버의 자원을 전혀 사용하지 않으며, 세션은 서버의 자원을 사용한다.
- **보안**
  - 쿠키는 클라이언트 로컬에 저장되기 때문에 변질되거나 request에서 스니핑 당할 우려가 있어서 보안에 취약하다. 반면 세션은 쿠키를 이용해서 세션 ID만 저장하고 그것으로 구분해서 서버에서 처리하기 때문에 비교적 보안성이 좋다.
- **라이프 사이클**
  - 쿠키는 만료시간이 있지만 파일로 저장되기 때문에 브라우저를 종료해도 계속해서 정보가 남아 있을 수 있다. 또한 만료 기간을 넉넉하게 잡아두면 쿠키 삭제를 할 때까지 유지될 수도 있다.
  - 반면, 세션도 만료시간을 정할 수 있지만 브라우저가 종료되면 만료시간에 상관없이 삭제된다.
- **속도**
  - 쿠키에 정보가 있기 때문에 서버에 요청 시 속도가 빠르다.
  - 반면 세션은 정보가 서버에 있기 때문에 처리가 요구되어 비교적 느린 속도를 낸다.
    - 세션은 서버의 자원을 사용하기 때문에 무분별하게 만들다 보면 서버의 메모리가 감당할 수 없어질 수가 있고 속도가 느려질 수 있기 때문에 쿠키를 함께 사용한다.

### 20. CORS가 무엇인가요?

**[CORS(Cross-Origin Resource Sharing)(교차 출처 리소스 공유)]**

- 다른 출처의 자원을 공유하도록 접근을 허용하는 것
- 추가적인 HTTP 헤더를 사용해 한 출처에서 실행중인 웹이 다른 출처의 선택한 자원에 접근할 권한을 부여하도록 브라우저에 알려주는 체제

**[CORS 동작 방식]**

- HTTP 프로토콜을 사용해 요청을 보낼 때에, 브라우저는 요청 헤더에 **Origin** 이라는 필드에 요청을 보내는 출처를 보냄
- 이후 서버 측에서 응답을 할 때, **Access-Control-Allow-Origin**이라는 값에 "리소스를 접근하는 것이 허용된 출처"를 보냄
- 이를 받은 브라우저는 본인이 보낸 Origin과 비교해 유효한 응답인지 결정

CORS의 시나리오로는 1) Preflight / 2) Simple / 3) Credentialed Request 가 있다.

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-17.png

1. **Preflight Request(예비 요청)**
   - 브라우저가 본 요청을 보내기 전에 보내는 요청
   - 서버는 예비 요청에 대한 응답으로 **허용/금지하는 정보**를 응답 헤더에 담아 보냄
   - 이후 브라우저는 Request와 Response의 허용 정책을 비교한 후, 안전하다고 판단되면 같은 end-point로 다시 본 요청을 보냄
   - 과정을 통해 브라우저 스스로 이 요청을 보내는 것이 안전한지 확인
2. **Credentialed Request(인증된 요청)**

   - 기존 예비요청에서 보안을 더 강화하고 싶을 때 사용하는 방식
   - 브라우저가 제공하는 비동기 리소스 요청 API, fetch API는 별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 X

   > **Credentials 옵션**

   요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션

   - **`same-origin(default)`**- 같은 출처 간 요청에만 인증 정보를 담을 수 있음
   - **`include`**- 모든 요청에 인증 정보를 담을 수 있음
   - **`omit`**- 모든 요청에 인증 정보를 담지 않음

**[CORS 이슈 해결방법]**

- Proxy 서버
  - 응답을 주고 받을때 프록시 서버에서 **`Access-Control-Allow-Origin: *`** 헤더를 담아 응답 (프록시 서버는 헤더를 추가하거나 요청을 허용/거부하는 역할을 중간에서 해줄 수 있음)

> **SOP란?**

**[SOP(Same-origin policy)(동일 출처 정책)]**

- **동일**한 출처(origin)에서만 리소스를 공유할 수 있다는 정책
- 다른 출처의 리소스를 사용하는 것을 제한하는 보안 방식

**`동일 출처`**

- protocol, host, port가 같아야 같은 출처임

**`예외`**

- CORS 정책을 지킨 리소스 요청
- 다른 출처에 있는 리소스를 가져와서 사용하는 일 多

### 21. IPv4와 IPv6 차이를 설명해주세요.

**IP는 Internet Protocol의 약자로 기기간 네트워크 통신을 할 때 쓰는 프로토콜을 의미**한다. IP에서 IP기기의 주소를 나타내는 것이 바로 IP주소이다. 데이터를 정확하게 송수신하기 위해서는 IP주소가 필요하다.

**IPv4**와 **IPv6**는 **인터넷 프로토콜(IP)의 버전**을 말한다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/ipv4-ipv6.png

### **[IPv6 개념 및 특징]**

- IP주소의 부족 현상을 해결하기 위한 차세대 IP주소체계
- IPv4의 주소 공간을 4배 확장한 것으로 128bit 체계의 16진수로 표기하며, 4개의 16진수를 콜론(:)으로 구분
- IPv4에서는 옵션 필드의 구성이 제한적인데 비해 IPv6에서는 확장헤더를 이용하여 IPv4보다 훨씬 다양하고 안정된 옵션을 사용할 수 있음
- 라우터의 부담을 줄이고, 네트워크 부하를 분산시킴
- 보안, 인증, 라벨링, 데이터 무결성, 데이터 비밀성 제공
- 특정 흐름의 패킷들을 인식하고, 확장된 헤더에 선택사항들을 기술할 수 있음
- IPv6 종류: 유니캐스트, 애니캐스트, 멀티 캐스트

### **[IPv4와 IPv6의 주요 차이점]**

**1. 보안강화**

- IPv6는 보안을 염두에 두고 구축되었기에 기밀성, 인증 및 데이터 무결성을 제공
- IPv4 구성 요소인 인터넷 제어 메시지 프로토콜(ICMP)은 멀웨어를 전달할 가능성이 있으므로 회사 방화벽에서 이를 종종 차단한다. 반면 IPv6 ICMP 패킷은 **IPSec**를 사용해 훨씬 더 안전하고 손쉽게 이를 막을 수 있다.

**2. 지리적 제한 없음**

- IPv4 주소와 달리 IPv6 주소는 전 세계 어느 곳에서도 사용할 수 있다.
- IPv4 주소의 50%는 생성될 때 미국에서 사용하는 용도로 예약되었다.

**3. 보다 효율적인 라우팅**

- IPv4 헤더는 길이가 가변적이지만 IPv6에는 일관된 헤더가 있다.
- 즉, 이러한 주소로 라우팅하기 위한 코드가 더 간단해지고 하드웨어 처리도 덜 필요하다.

**4. 끝과 끝 연결**

- 기술자들은 IP 주소 부족을 해결하기 위해 네트워크 주소 변환(NAT) 방법을 만들었다. 하지만 IPv6는 모든 장치에 대해 충분한 IP 주소를 생성하므로 NAT가 더 이상 필요하지 않게 되었다. 이제 각 장치가 인터넷에 연결되어 웹사이트와 직접 통신할 수 있게 되었다.

**5. 자동 구성**

- IPv6의 가장 좋은 기능 중 하나는 상태/비상태 유지 자동 저장 구성일 것이라고 한다. 이를 통해 장치는 서버 없이도 자체 IP주소를 할당할 수 있다. 대신 사용자가 소유한 모든 휴대폰, 태블릿 또는 노트북에 고유한 장치의 MAC 주소를 사용하여 IP주소가 생성된다. 이렇게 하면 동일한 네트워크에 연결된 장치가 서로를 더 쉽게 검색할 수 있다.

현재는 IPv4와 IPv6를 혼용해서 사용하는데, **IPv4 라우터에서는 tunneling이라는 방식을 사용해 IPv6 데이터그램을 전송한다.**

### **[IPv4에서 IPv6로 변환]**

| 구분      | 설명                                                                    |
| --------- | ----------------------------------------------------------------------- |
| 이중 스택 | 모든 인터넷이 IPv6를 사용하기 전까지 시스템은 IPv4와 IPv6를 동시에 지원 |
| 터널링    | - IPv6를 사용하는 두 호스트가 통신을 할 때,                             |

패킷이 IPv4를 사용하는 지역을 지나는 경우에 사용 가능한 방법

- IPv4 지역에 들어서면 IPv6 패킷은 IPv4 패킷으로 캡슐화되고 이 지역을 벗어날 때 역캡슐화 |
  | 헤더 변환 | - 인터넷의 대부분이 IPv6로 변경되고 일부만이 IPv4를 사용할 때 필요한 방법
- 헤더 변환을 통해 헤더의 형태를 완전히 변경 |

### 22. 서브네팅, 서브넷 마스크란 무엇인가요?

> **서브넷 마스크**

IP주소를 효율적으로 사용하여 낭비를 막기 위해서 네트워크 아이디와 호스트 아이디를 구별하는 구분자

Broadcast Domain에 많은 호스트가 연결된 경우 호스트에 발생한 Broadcast Traffic이 모든 호스트에 전달되어 많은 Broadcast Traffic이 발생한다.

하나의 Broadcast Domain 서는 보안이 취약하기 때문에 Firewall이나 ACL과 같은 정책을 구현하기 위해서는 Network Segment를 나누는 것이 효율적이다

**Subnet을 나누기 위한 작업:**

1. **Host or Subnet** 수를 파악 후 Subnetmask를 변경한다.
2. 변경된 1bit 부분을 2진수로 순서대로 쓴다.
3. 나온 수에 Host ID에 모두 0bit를 입력하면 Subnet에 Address가 나온다.
4. Host ID 부분을 모두 1bit로 처리 하면 Subnet Broadcast Address이다.

> **IP 주소와 서브네팅 (subnetting)**

IPv4 의 경우 232의 숫자로 주소를 표현하고, 이를 국가, 회사 등 잘게 나눠 어느 영역을 쓰게할 것인지 결정한다.

한정된 자원이기 때문에 효율적으로 노드에 주소를 할당하는게 중요하다. 이를 위해 IP 를 쪼개는, 네트워크 파트 + 호스트 파트로 구성하는 서브네팅을 활용한다.

기본적으로 IP 주소에 따라 5 개의 클래스로 구분된다. 각 클래스에 따라 네트워크 파트와 호스트 파트가 정해진다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/network-class.png

위와 같은 클래스 구조와 더불어 더욱 효율적인 서브네팅을 위해서 사용하는 방법이 서브넷 마스크이다.

> **서브넷 마스크 (subnet mask)**

할당된 IP 주소는 기본적으로 네트워크 파트와 호스트 파트가 정해져있다.

효율적인 주소 관리를 위해 내부적으로 호스트 파트를 새로운 네트워크 파트와 호스트 파트로 나눌 수 있다. 이 때 서브넷 마스크를 활용할 수 있다.

만약 C 클래스인 192.12.16.1 IP, 255.255.255.0 서브넷 마스크(호스트 파트)가 할당되었을 때 기존의 서브넷 마스크인 마지막 8 비트를 1111 0000 으로 바꾼다면, 4 비트만큼의 네트워크 파트 (그룹), 4 비트만큼의 호스트 (멤버) 를 할당할 수 있다. 이렇게 된다면 동일 네트워크 간에는 커뮤니케이션이 자유롭지만, 다른 네트워크 간에는 라우터를 거쳐야 커뮤니케이션을 할 수 있다.

어떤 기업을 생각해보자. 서브넷 마스크로 추가적인 서브네팅을 안한다면 인사팀, 재무팀 등등 여러 팀들이 모두 같은 네트워크 파트를 지니므로 서로에게 접근할 수 있다. 이럴 때 서브넷 마스크를 활용한 서브네팅으로 효율적으로 IP 를 관리할 수 있다.

### 22. MAC Address란 무엇인가요?

**`MAC 주소(Media Access Control Address)`**는 데이터 링크 계층에서 통신을 위해 **네트워크 인터페이스에 할당한 식별자**를 말한다. 즉, 모든 네트워크 장비는 자신의 MAC 주소가 있으며 주소는 장비 제조업체가 할당한다. MAC 주소는 물리적 주소라고 불리기도 한다.

> **💡 MAC 주소와 IP 주소의 차이**

MAC 주소와 IP 주소 모두 통신 기기의 식별자라는 것은 동일하다.

MAC 주소는 제조업체가 통신기기에 부여하는 식별자이며 같은 식별자를 같는 통신기기는 없다.

IP 주소는 네트워크 계층에서 통신을 하기 위한 주소로 보통 통신사에서 부여하며 바뀔 수 있다.

### 23. 라우터, 스위치, 허브의 차이를 설명해주세요.

(여기서의 네트워크는 LAN(Local Area Network))

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/router-switch-hub.png

**`라우터(Router)`**는 네트워크 계층 장비로 **네트워크 사이를 연결하는 장치**이다.

최종 도착지의 네트워크에 도착할 수 있도록 수신한 패킷의 정보를 보고 경로를 설정해 패킷을 전송한다.

**`스위치(Switch)`**는 데이터 링크 계층 장비로 **네트워크 내에서 패킷을 전송하는 장치**를 말한다.

스위치로 요청이 들어오면 IP 주소에 대응되는 MAC 주소를 찾아 해당 MAC 주소로 패킷을 전송한다. 만약 IP 주소에 대응되는 MAC 주소가 없다면 허브처럼 브로드캐스트 방식으로 패킷을 전송하고 IP 주소와 MAC 주소를 대응시킨 테이블을 갱신시킨다.

**`허브(Hub)`**는 물리 계층 장비로 **여러 기기를 연결하여 네트워크를 만들어주는 장치**이다.

패킷을 받으면 연결된 모든 기기에 패킷을 전송한다.

> **💡 브로드캐스트(Broadcast)란?**

브로드캐스트란 LAN에 있는 **모든** 네트워크 장비들에게 보내는 통신이다.

### 24. 이더넷(ethernet)이 무엇인가요?

이더넷은 원칙적으로 하나의 인터넷 회선에 유/무선 통신장비 공유기, 허브 등을 통해 다수의 시스템이 랜선 및 통신포트에 연결되어 통신이 가능한 네트워크 구조를 말한다. OSI 모델 7계층 중 물리 계층(신호와 배선)과 데이터 링크 계층(MAC 패킷, 프로토콜 형식)에서 그 구성 형식이 정의된다.

이더넷은 근거리 유선 통신을 위해 사용되는 네트워킹 방법으로 [CSMA/CD](https://security-nanglam.tistory.com/193)프로토콜을 사용한다. CSMA/CD 방법을 간략히 말하자면 버스 구조로 통신을 하는데 캐리어라는 네트워킹 상의 신호를 감지하여 캐리어가 없으면 정보를 보내는 방식이다.

- **장점**
  - 적은 용량의 데이터를 보낼 때 성능이 좋다.
  - 비용이 적고 관리가 쉽다.
  - 구조가 단순하다.
- **단점**
  - 캐리어 충돌이 발생할 수 있다.
  - 충돌이 발생하면 지연이 생긴다.

### 25. 라우팅 프로토콜을 몇 가지 설명해주세요.

패킷을 전달할 때 어느 경로로 갈지 정하는 것을 라우팅이라고 한다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/routing.png

> **라우팅 경로 고정 여부**

어떤 경로로 라우팅할지 사전 정의 여부에 따라 `정적 라우팅`, `동적 라우팅` 으로 구분한다.

> **내/외부 라우팅**

동적 라우팅에서  `내부 라우팅` (RIP, IGRP, OSPF, EIGRP) 과 `외부 라우팅` (BGP, EGP) 으로 나눈다.

## RIP(Routing Information Protocol)

- 최소 Hop count를 파악하여 라우팅하는 프로토콜이다.
- 거리와 방향으로 길을 찾아가는 Distance Vector 다이나믹 프로토콜이다.
- 최단거리 즉, Hop count가 적은 경로를 택하여 라우팅하는 프로토콜로 Routing Table에 인접 라우터 정보를 저장하여 경로를 결정한다.
- 최대 Hop count는 15로 거리가 짧기 때문에 IGP로 많이 이용하는 프로토콜이다.
- 라우터의 메모리를 적게 사용하며, 30초마다 라우팅 정보를 업데이트 한다.
- Hop count가 낮을수록 좋은 경로, 소규모 네트워크에서 간편하게 구성 가능하다.
- 4~6개까지 로드 밸런싱이 가능하다.
- 주로 UDP 세그먼트에 캡슐화되어 사용한다.
- RIP는 단순 Hop을 count하여 경로를 결정하기 때문에 경로의 네트워크 속도는 판단하지 않는다. 비효율적인 경로로 패킷을 전달할 가능성이 있다.
- Distance Vector 알고리즘으로 네트워크 변화에 대처하는 시간(컨버전스 타임)이 느리다는 단점이 있다.

## BGP(Border Gateway Protocol)

- BGP는 외부 라우팅 프로토콜로(EGP) AS(관리 도메인)와 AS간에 사용되는 라우팅 프로토콜이다.
- 정해진 정책에 따라 최적 라우팅 경로를 수립한다.
- 경로벡터(Distance Vector) 방식의 라우팅 프로토콜로 다른 IGP보다 컨버전스는 느리지만 대용량의 라우팅 정보를 교환할 수 있다.

## OSPF(Open Shortest Path First)

- 최단 경로 우선 프로토콜이다.
- 최저 COST(최저 시간) 경로를 최적 라우팅 경로로 결정한다.
- 가장 대표적인 링크 상태 프로토콜로 SPF(최단거리우선 알고리즘)을 통해 라우팅 테이블을 생성한다.
- Area 개념을 사용하여 전체 네트워크를 작은 영역으로 나눠 효율적으로 관리한다.
- RIP가 30초마다 업데이트 되어 정보를 전송시키는 반면, **OSPF는 링크에 상태변화가 있을 시에 즉각적으로 Flooding을 해주어 컨버전스 타임이 매우 빠르다.**

> 라우팅 알고리즘 비교

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0429f1cd-559a-4734-9211-1082fe609a9d/6461baa9-4cf2-4d1e-937f-7eb0b4277781/image.png)

### 26. 공인(public) IP와 사설(private) IP의 차이에 대해 설명해주세요.

- **공인 IP**
  - 전세계에서 유일한 IP로 ISP(인터넷 서비스 공급자)가 제공하는 IP주소
  - 외부에 공개되어 있기 때문에 인터넷에 연결된 다른 장비로부터 접근이 가능하다.
  - 그에 따라 방화벽 등과 같은 보안 설정을 해주어야 한다.
- **사설 IP**
  - 어떤 네트워크 안에서 사용되는 IP주소
  - IPV4의 부족으로 인해 모든 네트워크가 공인 IP를 사용하는 것이 불가능하기 때문에 네트워크 안에서 라우터를 통해 할당받는 가상의 주소이다.
  - 별도의 설정 없이는 외부에서 접근이 불가능하다.

### 27. 프록시 서버의 개념과 기능에 대해 설명해주세요.

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-14.png

- 클라이언트가 자신을 거쳐 다른 네트워크에 접속할 수 있도록 중간에서 대리해주는 서버
- 서버와 클라이언트 사이에서 대리로 통신을 수행해주는 것을 프록시라고 하고 그 기능을 하는 서버를 프록시 서버
- 서버와 클라이언트 사이에서 요청과 응답을 처리

**[통신 과정]**

1. 클라이언트에서 프록시 서버로 데이터 전송
2. 프록시 서버에서 다시 웹 서버로 웹 요청
3. 웹 서버에서 프록시 서버로 웹 응답
4. 프록시 서버에서 클라이언트로 데이터 전송

**[사용 목적]**

- **캐시 데이터 사용**
  - 일부 프록시 서버는 요청된 내용을 캐시로 저장 → 캐시에 저장되어있는 내용에 대한 재요청은 서버에 따로 접속할 필요 X (저장된 내용을 그대로 돌려줌)
  - 전송 시간 절약, 외부 트래픽 줄어듬 → 네트워크 병목 현상도 방지
- 보안 (프록시 방화벽)
  - 중간에 프록시 서버에 경유하면 IP를 숨길 수 있음 → 방화벽으로 사용되기도 함
- **접속 우회**
  - 우회에 사용할 서버 주소와 포트를 설정해주면 설정한 서버에서 접속한 것처럼 속일 수 있음

### 28. 패킷교환/회선교환을 비교/설명해주세요.

### 29. SMTP는 무엇인가요?

**`SMTP(Simple Mail Transfer Protocol)`**은 **인터넷에서 이메일을 보내기 위해 사용하는 TCP/IP 프로토콜**을 말한다. 사용하는 TCP Port 번호는 25번이다.

### 30. 데이터 캡슐화와 역캡슐화는 무엇인가요?

데이터 캡슐화는 데이터를 보내는 송신 측에서 데이터를 생성하는 방법으로, 네트워크 계층에서 상위 계층에서부터 하위 계층으로 내려올 때마다 각 계층의 헤더를 붙여 보내는 데이터로 만들어낸다.

반대로 데이터를 받는 수신측에서는 데이터를 받은 후에 계층을 거슬러 올라가면서 헤더를 떼내며 데이터를 파악하는데 이를 데이터 역캡슐화라고 한다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/data-encapsulation.png

### 31. 소켓(socket)이 무엇인가요?

`소켓(Socket)`이란 애플리케이션 프로세스와 end-to-end 통신을 제공하는 전송 프로토콜 사이의 인터페이스을 말한다. 즉, 애플리케이션에서 전송 프로토콜을 쓰기 위한 API를 말한다.

### 31-1. Socket.io와 WebSocket의 차이를 설명해주세요.

> **WebSocket**

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/web-socket.png

**`WebSocket`**은 서버와 브라우저 간 연결을 유지한 상태로 데이터를 교환할 수 있도록 하는 **프로토콜**을 말한다. 즉, 브라우저와 서버 간 **양방향** 메시지 송수신 규칙이다.

> **Socket.io**

**`socket.io`**는 서버와 브라우저의 양방향 통신을 가능하게 하는 **모듈**을 말한다.

WebSocket의 경우, 오래된 브라우저는 지원을 하지 않는 경우가 있다. 이런 경우 socket.io는 서버와 브라우저의 종류와 버전을 파악하여 가장 적합한 기술을 선택해 양방향 통신이 가능하도록 한다.

### 32. Delay, Timing, Throughput의 개념을 설명해주세요.

위 세가지 개념은 모두 네트워크의 성능과 관련되어 있다.

> **delay**

하나의 데이터 패킷이 출발 지점에서 도착 지점에 도착한 시간을 의미한다.

- **`처리 지연`:** 라우터가 들어온 패킷의 헤더를 확인하고 처리하는데 걸리는 시간
- **`큐 지연`:** 라우터가 다른 패킷을 처리하느라 패킷이 라우터의 큐에서 대기하는 시간
- **`전송 지연`:** 라우터의 성능(전송 속도) 에 따라 패킷이 논리회로를 통과할 때까지 걸리는 시간
- **`전파 지연`:** 라우터간 거리에 의해 발생하는 지연 시간

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/network-delay.png

> **timing(jitter)**

delay 의 변동을 (변화량 수준) 의미한다. 같은 스위치가 아닌 경우 패킷마다 대기 시간이 달라지므로 **jitter**가 생긴다.

> **throughput**

지정된 시간동안 실제로 전송된 정보량을 의미한다.

### 33. 로드 밸런싱은 무엇인가요?

!https://github.com/kuS2-computer-princess-kuS2/cs_study/raw/HS/HS/Network/image-8.png

- 특정 서버 또는 네트워크 허브에 부하가 집중되지 않도록 트래픽을 분산시키는 것
  - 로드밸런서는 클라이언트의 요청 및 네트워크의 트래픽이 집중되는 서버 또는 네트워크 허브 사이에 위치하여 로드밸런싱 수행
- 효과: 가용성 및 응답시간 최적화

**[로드밸런싱의 기능]**

1. Health Check (상태 확인)
   - 서버들에 대한 주기적인 상태 확인을 통해 서버들의 장애 여부를 판단하여, 정상 동작 중인 서버로만 트래픽을 보냄
2. Tunneling (터널링)
   - 데이터 스트림을 인터넷 상에서 가상의 파이프를 통해 전달시키는 기술
   - 연결된 상호 간에만 캡슐화된 패킷을 구별해 해제하게 함
3. NAT (Network Address Translation)
   - 내부 네트워크에서 사용하는 사설 IP 주소와 로드밸런서 외부의 공인 IP 주소 간의 변환 역할
   - 목적: 여러 개의 호스트가 하나의 공인 IP 주소를 통해 접속하는 것
4. DSR (Destination Network Address Translation)
   - 서버에서 클라이언트로 트래픽이 되돌아가는 경우, 네트워크 장비나 로드밸런서를 거치지 않고 바로 클라이언트를 찾아가는 방식 -> 로드밸런서의 부하 줄임

**[로드밸런싱 알고리즘]**

1. 라운드 로빈 방식
   - 서버로 들어온 요청을 순서대로 돌아가며 배정하는 방식
2. IP 해시 방식
   - 클라이언트의 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식
3. 최소 연결 방식 (Least Connection Method)
   - 요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽 할당하는 방식
4. 최소 응답시간 방식 (Least Response Time Method)
   - 서버의 현재 연결 상태와 응답시간을 모두 고려하여, 가장 짧은 응답 시간을 보내는 서버로 트래픽을 할당하는 방식

### 34. ARP란 무엇인가요?

네트워크 상에서 IP주소를 물리적 주소로 대응시키기 위해 사용되는 주소 결정 프로토콜이다.

ARP를 사용하는 이유는 로컬 네트워크(LAN)에서 단말과 단말 간 통신을 하기 위해서는 IP 주소와 함께 MAC 주소를 이용하게 되는데, IP 주소를 MAC Address와 매칭하여 목적지 IP의 단말이 소유한 MAC 주소를 향해 제대로 찾아가기 위함이다.

### 35. 여러 네트워크 토폴로지(topology)에 대해 간단히 소개해주세요.

컴퓨터끼리 정보를 교환하고 교류하는 형태를 의미하는 네트워크에서 토폴로지는 **컴퓨터들의 특정한 망구성 방식**을 의미한다.

> **Star**

중앙에 위치한 메인 노드를 통해 다른 노드와 소통할 수 있는 구조이다.

- `장점`: 장애 발견이 쉽고 관리가 용이함
- `단점`: 메인 노드에 장애가 발생하면 전체 네트워크 사용 불가능

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/star-topology.png

> **Bus**

버스라는 공통 배선을 통해 노드들이 연결되어 있어서, 한 노드의 신호가 모든 노드에 전달된다. (타겟 노드만 신호에 반응을 하고 다른 노드는 무시한다.)

- `장점`: 노드 추가 및 삭제가 용이하며, 한 노드에 장애가 발생해도 다른 노드에 영향을 주지 않음
- `단점`: 공통 배선의 크기(대역폭)가 제한되어 있으므로 배선에 과부하가 걸릴 경우 네트워크 성능 저하

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/bus-topology.png

> **Ring**

각 노드가 양 옆으로 연결된 원형 구조, 단방향으로 신호가 전달된다.

- `장점`: 단방향 구조로 단순하고, 중간에 있는 노드들이 증폭기의 역할을 해준다. (거리 제약 적어진다.)
- `단점`: 노드 추가 및 삭제가 어렵다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/ring-topology.png

> **Mesh**

다수의 노드가 서로 연결된 형태이다. (모두 연결되면 완전 연결형, 일부만 연결되면 부분 연결형)

- `장점`: 노드의 장애에 영향받지 않으며 유연한 대처가 가능하고 안정적이다.
- `단점`: 구축 비용이 크고, 노드 추가에도 비용이 많이 든다.

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/mesh-full-topology.png

!https://github.com/boost-devs/ai-tech-interview/raw/main/answers/img/5-network/mesh-part-topology.png

---

### 36. 세션 기반 인증과 토큰 기반 인증의 차이에 대해 얘기해주세요.

세션 기반 인증은 클라이언트로부터 요청을 받으면 클라이언트의 상태 정보를 저장하므로 Stateful한 구조를 가지고, 토큰 기반 인증은 상태 정보를 서버에 저장하지 않으므로 Stateless한 구조를 가집니다.

### 36-1. 그렇다면 Stateful한 세션 기반의 인증 방식을 사용하게 된다면 어떠한 단점이 있을까요?

1. 서버에 세션을 저장하기 때문에 사용자가 증가하면 서버에 과부하를 줄 수 있어 확장성이 낮습니다.

2. 해커가 훔친 쿠키를 이용해 요청을 보내면 서버는 올바른 사용자가 보낸 요청인지 알 수 없습니다. (세션 하이재킹 공격)

### 36-2. 그렇다면 세션 기반 인증과 토큰 기반 인증은 각각 어느 경우에 적합한가요?

단일 도메인이라면 세션 기반 인증을 사용하고, 아니라면 토큰 기반 인증을 사용하는 것이 적합하다고 생각합니다.

왜? - 세션을 관리할 때 사용되는 쿠키는 단일 도메인 및 서브 도메인에서만 작동하도록 설계되어 있기 때문에 여러 도메인에서 관리하는 것은 어렵습니다. (CORS 문제)

### 36. JWT 토큰에 대해 설명해주세요.

JWT는 JSON 포맷을 이용하는 Claim 기반의 웹 토큰이며, 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달합니다.

JWT는 헤더(Header).내용(Payload).서명(Signature)로 구성되며 각 파트를 점(.)으로 구분합니다.

- **헤더(Header)** : 토큰의 타입과 해시 암호화 알고리즘(방식지정)으로 이루어져 있다.
- **내용(Payload)** : 토큰에 사용자가 담고자 하는 정보를 담는다. 내용에는 Claim이 담겨있고, JSON(Key/Value)형태의 한 쌍으로 이루어져 있다.
- **서명(Signature)** : 토큰을 인코딩하거나 유효성 검증할 때 사용하는 고유한 암호화 코드이다. 헤더와 내용의 값을 인코딩한다.

### 37. HTTP 1 vs HTTP 2

!https://blog.kakaocdn.net/dn/tp1sd/btrozjn33FT/iGKn5OEnfk5oD3uHsPM3fK/img.png

1. **`HTTP1`**는 연결 당 하나의 요청/응답을 처리하여 상당히 비효율적인 방식이였음
   - RTT(Round Trip Time) 증가: 패킷 왕복 시간의 지연 발생
2. **`HTTP1.1`**는 지속 연결(Persistence Connection)과 파이프라이닝 등으로 보완했지만 한계 존재
   - HOL(Head Of Line) Blocking: 클라이언트의 요청과 서버의 응답이 동기화되어 지연 발생(여러 요청을 동시에 보내지만 첫 요청이 끝나지 않으면 나머지 요청도 블로킹 됨)
   - 헤더 크기의 비대: 연속된 요청에 대해 동일한 헤더를 전송하게 됨
3. **`HTTP2`**는 아래의 기술을 사용하여 HTTP1의 성능 문제를 해결하였음
   - Multiplexed Streams: 하나의 커넥션으로 여러 개의 메세지를 순서 상관없이 동시에 주고 받을 수 있음
   - Stream Prioritization: 리소스간의 전송 우선 순위를 설정할 수 있음
   - Header Compression: 헤더 정보를 HPACK 압축 방식을 이용하여 압축 전송함, HPack은 허프만을 사용함
   - Server Push: HTML문서 상에 필요한 리소스를 클라이언트 요청없이 보내줄 수 있음
4. **`HTTP3`**는 아래의 특징을 갖고 있음
   - QUIC라는 계층 위에서 돌아가며, 이는 UDP를 기반으로 돌아감(RTT 감소)
   - 순방향 오류 수정 메커니즘(FEC, Forworad Error Correction)으로 전송한 패킷이 손실되었다면 수신 측에서 에러를 검출하고 수정하는 방식

### 38. VLAN이란?

### 39. 싱글스레드 서버와 멀티스레드 서버 예시

### 40. ARQ란?

### 41. DHCP란?

DHCP (Dynamic Host Configuration Protocol) 는 동적으로 IP 주소나 기타 정보들을 관리해주는 프로토콜을 말한다. 관리해야하는 컴퓨터가 많고 이들의 IP 를 모두 직접 할당하고 관리하려면 상당히 복잡하고 시간이 많이들지만, DHCP 를 사용하면 이러한 문제점을 해결할 수 있다.

DHCP 는 UDP 를 사용하여 클라이언트/서버 구조로 통신한다. 그 과정은 아래와 같다.

1. `DHCP discover`: 컴퓨터가 동일 서브넷으로 브로드캐스팅(255.255.255.255)으로 DHCP 서버를 찾는다.
2. `DHCP offer`: DHCP 가 사용가능한 IP 주소의 리스트를 컴퓨터에게 전달한다.
3. `DHCP request`: 컴퓨터가 리스트 중 하나의 IP 주소를 선택하여 서버에 전달한다.
4. `DHCP ack`: DHCP 가 컴퓨터에게 해당 IP 주소를 허락/거절하는 메세지를 전달한다.

> 장점

- DHCP 서버에서 자동으로 IP 를 관리해주므로 편리하다. IP 에 변동이 있을 때, DHCP 에만 정보를 입력하면 된다.
- 사용중인 컴퓨터에 대해서만 할당하므로 효율적이다.

> 단점

- DHCP 서버에 의존하기 때문에 서버가 다운되는 경우 모든 컴퓨터에서 인터넷을 할 수 없다.
- 초기 DHCP 세팅 시간 및 트래픽이 크다.
- 단말 컴퓨터를 끌 경우, 완전히 주소가 release 될 때 까지 해당 IP 를 사용할 수 없다.

### 42. unicast, multicast, broadcast 설명

### 43. XSS란?

### 44. ATM이란?

### **45. IOCP를 설명하시오**

IOCP는 어떤 I/O 핸들에 대해, 블록 되지 않게 비동기 작업을 하면서 프로그램 대기시간을 줄이는 목적으로 사용된다.

동기화 Object 세마포어의 특성과, 큐를 가진 커널 Object다. 대부분 멀티 스레드 상에서 사용되고, 큐는 자체적으로 운영하는 특징 때문에 스레드 풀링에 적합함

동기화와 동시에 큐를 통한 데이터 전달 IOCP는, 스레드 풀링을 위한 것이라고 할 수 있음

### **46. POOLING이란?**

여러 스레드를 생성하여 대기시키고, 필요할 때 가져다가 사용한 뒤에 다시 반납하는 과정 (스레드의 생성과 파괴는 상당히 큰 오버헤드가 존재하기 때문에 이 과정을 이용한다)

IOCP의 장점은 사용자가 설정한 버퍼만 사용하기 때문에 더 효율적으로 작동시킬 수 있음. (기존에는 OS버퍼, 사용자 버퍼로 따로 분리해서 운영했음)

커널 레벨에서는 모든 I/O를 비동기로 처리하기 때문에 효율적인 순서에 따라 접근할 수 있음

### 47. Connection Timeout과 Read Timeout의 차이에 대해 설명해주세요.

서버 자체에 클라이언트가 어떤 사유로 접근을 실패했을 시 적용되는 것이 Connection Timeout입니다.즉, 접근을 시도하는 시간 제한이 Connection Timeout 되는 것을 말합니다.

클라이언트가 서버에 접속을 성공 했으나 서버가 로직을 수행하는 시간이 너무 길어 제대로 응답을 못 준 상태에서 클라이언트가 연결을 해제하는 것이 Read Timeout입니다.

이 경우는 클라이언트는 해당 상황을 오류로 인지하고, 서버는 계속 로직을 수행하고 있어 성공으로 인지해, 양 사이드간 싱크가 맞지 않아 문제가 발생할 확률이 높습니다.

### 48. SYN Flooding 공격 설명, 방어 방법

client가 server로 연결 요청(SYN)을 보내면 server가 백로그 큐에 저장하는데, 큐가 가득 차게 되면 더 이상 요청을 받을 수 없게 된다. Denial of Service(Dos) attack 중 하나이다.

**해결방법**

1. Cookie 사용: 서버가 SYN+ACK 메시지를 보낼 때 SYN Cookie도 함께 보낸다. 일정 시간 동안 해당 쿠키에 대한 응답 패킷이 오지 않는다면 방화벽에서 차단한다.

2. 타임아웃 시간을 짧게 잡아 백로그 큐를 계속해서 비워줄 수 있다.

\*_참고 레퍼런스_

https://mangkyu.tistory.com/91
https://dev-coco.tistory.com/161
https://kjsu0209.github.io/Tech-Interview/network/network
https://gyoogle.dev/blog/interview/네트워크.html
https://github.com/boost-devs/ai-tech-interview/blob/main/answers/5-network.md#31
