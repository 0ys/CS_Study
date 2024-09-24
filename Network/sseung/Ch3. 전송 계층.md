## **3.1 Introduction and Transport-Layer Services**

### **3.1.1 Relationship Between Transport and Network Layers**

### **3.1.2 Overview of the Transport Layer in the Internet**

---

## **3.2 Multiplexing and Demultiplexing**

- 역다중화(demultiplexing) : 트랜스포트 계층 세그먼트의 데이터를 올바른 소켓으로 전달하는 작업, 패킷을 수신하는 쪽에서 일어남
- 다중화(multiplexing) : 출발지 호스트에서 소켓으로부터 데이터를 모으고, 이에 대한 세그먼트를 생성하기 위해서 각 데이터에 헤더 정보(나중에 역다중화에 사용된다)로 캡슐화하고, 그 세그먼트들을 네트워크 계층으로 전달하는 작업, 패킷을 전단하는 쪽에서 일어남

**트랜스포트 계층 다중화 요구사항**

1. 소켓은 유일한 식별자(포트)를 가짐

2. 각 세그먼트는 세그먼트가 전달된 적절한 소켓을 가리키는 특별한 필드를 가짐

→ 특별한 필드 : 출발지 포트 번호 필드(source port number field), 목적지 포트 번호 필드(destination port number field)

**비연결형(UDP) 다중화와 역다중화**

- 목적지 포트 번호와 목적지 IP주소를 통해서 목적지 프로세스를 특정
- 출발지 포트 번호는 "복귀 주소"의 한 부분으로 사용
- UDP 소켓은 'IP주소'와 '목적지 포트 번호'로 구성된 두 요소로 된 집합에 의해서 식별
    
    → 목적지 IP와 포트 번호가 같으면 같은 소켓으로 취급
    
![image](https://github.com/user-attachments/assets/7d5cee3e-c95f-4fca-bda2-169b28092ea3)
    

**연결지향형(TCP) 다중화와 역다중화**

- TCP 소켓은 4개 요소들의 집합(출발지 IP주소, 출발지 포트 번호, 목적지 IP주소, 목적지 포트 번호)에 의해서 식별
- 서버 호스트는 동시에 존재하는 많은 TCP 소켓을 지원할 수 있다
    
    → 목적지IP와 포트 번호가 같아도 다른 요소(출발지 IP주소, 출발지 포트번호)가 다르다면 다른 소켓으로 취급 
    
![image](https://github.com/user-attachments/assets/3620f2a7-01f8-47ca-b891-ff61d4daa3ab)

---

### **3.3 Connectionless Transport: UDP**

### **3.3.1 UDP Segment Structure**

### 3.3.2 UDP 체크섬

---

### **3.4 Principles of Reliable Data Transfer**

### 3.4.1 신뢰적인 데이터 전달 프로토콜의 구축

### **3.4.2 Pipelined Reliable Data Transfer Protocols**

### **3.4.3 Go-Back-N (GBN)**

### **3.4.4 Selective Repeat (SR)**

---

### **3.5 Connection-Oriented Transport: TCP 

### **3.5.1 The TCP Connection**

- TCP는 애플리케이션 프로세스가 데이터를 전송하기 전에 두 프로세스가 서로 "핸드셰이크"
    
    → 연결 지향적
    
- TCP 프로토콜은 중간 네트워크 요소(라우터 및 링크 계층 스위치)에서는 실행되지 않고 종단 시스템에서만 실행 → 중간 네트워크 요소는 TCP 연결 상태를 유지 X
- TCP 연결은 p2p로 1:1의 관계로 성립, 1:다 → 불가능
- 클라이언트가 먼저 특수한 TCP 세그먼트를 보냄
    
    → 서버가 두 번째 특수한 TCP 세그먼트로 응답
    
    → 마지막으로 클라이언트가 세 번째 특수한 세그먼트로 다시 응답
    
- 처음 두 세그먼트는 페이로드, 즉 애플리케이션 계층 데이터 X, 세 번째 세그먼트는 페이로드 O
    
    → TCP 연결이 설정되면 두 애플리케이션 프로세스는 서로 데이터 전송 가능
    

### **3.5.2 TCP Segment Structure**

![image](https://github.com/user-attachments/assets/6e6d034a-4828-41bf-9498-329676541107)

- **헤더 필드**
    - 응용 프로그램 데이터의 청크를 포함
    - **`소스 및 목적지 포트 번호` →** 상위 계층 응용 프로그램으로의 데이터 다중화 및 역다중화에 사용
    - **`체크섬 필드`** 가짐
- **데이터 필드**
- **`MSS`**
    - 세그먼트 데이터 필드의 최대 크기 제한
    - TCP가 큰 파일을 전송할 때, 일반적으로 파일을 MSS 크기의 청크로 나눔
- **`시퀀스 번호 필드`**와 **`확인 응답 번호 필드`(ack)**
    - TCP 송신자와 수신자가 신뢰할 수 있는 데이터 전송 서비스를 구현하는 데 사용
- **`수신 윈도우 필드`**
    - 흐름 제어
    - 수신자가 수용할 수 있는 바이트의 수
- **`헤더 길이 필드`**
    - TCP 헤더의 길이
    - TCP 옵션 필드 → TCP 헤더는 가변 길이를 가질 수 있음
- **`옵션 필드`**
    - 선택적, 가변 길이를 가짐
    - 송신자와 수신자가 최대 세그먼트 크기(MSS)를 협상하거나 고속 네트워크에서 사용할 창 확장 인자로 사용
    - 타임스탬프 옵션 정의
- **`플래그 필드`**
    - 성공적으로 수신된 세그먼트에 대한 확인 응답
- **`RST`**, **`SYN`**, **`FIN`** 비트
    - 연결 설정 및 종료에 사용
- **`CWR`** 및 **`ECE`** 비트는 명시적 혼잡 알림에서 사용
- **`PSH`** 비트
    - 수신자가 데이터를 상위 계층에 즉시 전달해야 함을 나타냄
- **`URG`** 비트
    - 송신 측 상위 계층 엔터티가 "긴급"으로 표시한 데이터가 이 세그먼트에 포함되어 있음을 표현
- **`긴급 데이터 포인터 필드`**
    - TCP는 수신 측 상위 계층 엔터티에 긴급 데이터가 존재함을 알려야 하며, 긴급 데이터의 끝에 대한 포인터를 전달해야 함

### 시퀀스 번호와 확인 응답 번호 필드

- TCP의 신뢰할 수 있는 데이터 전송 서비스의 중요한 부분
- TCP는 데이터를 구조화되지 않은, 하지만 순서가 있는 바이트 스트림으로 여김
- **시퀀스 번호**
    - 전송된 바이트 스트림에 대한 것 (세그먼트 X)
    - 세그먼트의 시퀀스 번호 → 해당 세그먼트의 첫 번째 바이트의 바이트 스트림 번호
- **확인 응답 번호**
    - TCP는 전이중(Full-duplex)임
    - 호스트 A와 호스트 B 쌍방 데이터 전송하는 경우
        - 호스트 A가 자신의 세그먼트에 넣는 확인 응답 번호는 호스트 A가 호스트 B로부터 기대하고 있는 다음 바이트의 시퀀스 번호
- TCP 연결의 양측은 무작위로 초기 시퀀스 번호를 선택
    
    → 두 호스트 간의 이전에 종료된 연결에서 네트워크에 아직 남아 있는 세그먼트가 이후의 연결(이전 연결과 동일한 포트 번호를 사용하는 경우)에서 유효한 세그먼트로 오인될 가능성을 최소화하기 위함
    

**3.5.3 Round-Trip Time Estimation and Timeout** 

- 손실된 세그먼트를 복구하기 위해 타임아웃/ 재전송 메커니즘을 사용

### 왕복 전송 시간 추정

- 송신자와 수신자 사이의 왕복 전송 시간?
    - 세그먼트에 대한 **샘플 RTT(SampleRTT)**는 세그먼트가 전송될 때부터 세그먼트에 대한 확인 응답이 수신될 때까지의 시간
    - 대부분의 TCP 구현에서는 전송된 모든 세그먼트에 대해 SampleRTT를 측정하지 않고, 한 번에 하나의 SampleRTT 측정
    - 즉, 어느 시점에서든지 SampleRTT는 전송되었으나 아직 확인되지 않은 세그먼트 중 하나에 대해서만 추정되며, 약 매 RTT마다 새로운 SampleRTT 값을 얻음
    - TCP는 재전송된 세그먼트에 대해 SampleRTT를 절대 계산하지 않으며, 한 번 전송된 세그먼트에 대해서만 SampleRTT를 측정
    - SampleRTT 값은 라우터의 혼잡 및 종단 시스템의 부하 변화로 인해 세그먼트마다 변동
        
        → 특정 SampleRTT 값은 전형적 X → SampleRTT 값의 평균 사용 → **추정 RTT(EstimatedRTT)**
        
        - **`*EstimatedRTT=0.875*⋅*EstimatedRTT+0.125*⋅*SampleRTT*`**
- EstimatedRTT는 SampleRTT 값의 가중 평균
    - 최신 샘플에 이전 샘플보다 더 많은 가중치를 부여?
        - 최근 샘플이 네트워크의 현재 혼잡 상태를 더 잘 반영 → **지수 가중 이동 평균(EWMA)**
- **DevRTT**
    - SampleRTT가 EstimatedRTT에서 일반적으로 얼마나 벗어나는지를 추정하는 값
    - **`*DevRTT=(1−β)*⋅*DevRTT+β*⋅*|SampleRTT−EstimatedRTT|*`**
    - SampleRTT와 EstimatedRTT 간의 차이의 EWMA
    - SampleRTT 값이 거의 변동 X → DevRTT는 작음
    - 변동이 많으면 DevRTT는 커짐

### 재전송 타임아웃 간격 설정 및 관리

- **TCP의 타임아웃 간격 (**TimeoutInterval)
    - **`*TimeoutInterval=EstimatedRTT+4*⋅*DevRTT*`**
    - **EstimatedRTT보다 작다면?** → 불필요한 재전송이 발생
    - **EstimatedRTT보다 너무 크면?**
        
        → 세그먼트가 손실될 때 세그먼트를 신속하게 재전송하지 않아 큰 데이터 전송 지연 초래
        
    - **DevRTT 사용하는 이유**
        - SampleRTT 값에 변동 多 → 여유⬆ , 변동⬇ → 여유⬇
    - **`타임아웃이 발생`**
        - 곧 확인될 세그먼트에 대해 조기 타임아웃을 방지 → TimeoutInterval 값이 두 배 ⬆
            
            → 그러나 세그먼트가 수신되고 EstimatedRTT가 업데이트 → TimeoutInterval 재연산
            

### **3.5.4 Reliable Data Transfer**

- TCP는 IP의 신뢰할 수 없는 최선의 노력 서비스 위에 신뢰할 수 있는 데이터 전송 서비스를 구축
    - 프로세스가 TCP 수신 버퍼에서 읽어들인 데이터 스트림이 손상되지 않고, 중간에 데이터가 빠지거나 중복되지 않으며, 순서가 유지됨을 보장
- **TCP 타이머 관리 절차**
    - 아직 확인되지 않은 여러 세그먼트가 있더라도 단일 재전송 타이머만 사용

**`시나리오1`**

![image](https://github.com/user-attachments/assets/8a1e2e3f-7eb2-4ea6-8681-cd65b7d9a308)

- A로부터의 세그먼트는 B에서 수신, B에서 A로의 확인이 손실
    - 타임아웃 이벤트가 발생 → 호스트 A는 동일한 세그먼트를 재전송
    - 호스트 B가 재전송을 수신하면 시퀀스 번호로부터 이미 수신된 데이터임을 인지
        
        → 호스트 B 재전송된 세그먼트의 바이트 폐기
        

**`시나리오2`**

![image](https://github.com/user-attachments/assets/3656a5dc-d5bc-41bc-a088-92ee7304c77f)

- **호스트 A가 두 세그먼트를 연속으로 보내는 경우**
    
    → 두 개의 ACK이 모두 타임아웃 전에 호스트 A에 도착하지 않을 때
    
    - 타임아웃 이벤트가 발생 → 호스트 A는 시퀀스 번호 92인 첫 번째 세그먼트 재전송
        
        → 두 번째 세그먼트에 대한 ACK가 새로운 타임아웃 전에 도착? 
        
        → 두 번째 세그먼트는 재전송 X
        

**`시나리오3`**

![image](https://github.com/user-attachments/assets/7070d7a0-de58-47d1-8c92-3f20af9e9f4b)

- **첫 번째 세그먼트의 확인이 네트워크에서 손실된 경우**
    
    → 타임아웃 이벤트 직전에 호스트 A는 확인 번호 120을 가진 ACK을 수신
    
    → 호스트 A는 두 세그먼트 중 어느 것도 재전송 X
    

### [해결책]

### `타임아웃 간격 두 배로 늘리기`

1. **타이머 만료 후 타임아웃 간격의 길이?**
    - 타임아웃 이벤트가 발생할 때마다 TCP는 아직 확인되지 않은 가장 작은 시퀀스 번호를 가진 세그먼트를 재전송
    - 타임아웃 간격을 이전 값의 두 배로 설정 → 재전송 후의 간격은 지수적으로 증가
    - timer 세팅 → TimeoutInterval은 가장 최근의 EstimatedRTT와 DevRTT 값에서 파생

### `빠른 재전송`

- 세그먼트가 손실되면 긴 타임아웃 기간은 송신자가 손실된 패킷을 재전송하는 데 지연을 초래 → 종단 간 지연을 증가
- **중복 ACK 확인**
    - 송신자가 이전에 수신한 세그먼트를 다시 확인하는 ACK
    - 타임아웃 이벤트가 발생하기 훨씬 전에 패킷 손실을 감지
- **수신자가 중복 ACK을 보내는 경우**
- TCP 수신자가 예상된 다음 순서의 시퀀스 번호보다 큰 시퀀스를 가진 세그먼트를 수신
    
    → 데이터 스트림의 간격, 즉 손실된 세그먼트를 감지
    
    - 이 간격은 네트워크 내에서 세그먼트가 손실되거나 순서가 변경된 결과
    - 수신자는 수신한 마지막 순서 바이트 데이터를 재확인(즉, 중복 ACK 생성)
    
![image](https://github.com/user-attachments/assets/28eca178-01f6-4342-a778-c6940e4694d2)
    
- 세그먼트 연속 전송 시, 세그먼트가 하나 손실되면 중복 ACK이 대량으로 발생할 가능성 ⬆
    - TCP 송신자가 동일한 데이터에 대해 세 번의 중복 ACK을 받으면, 이는 송신자가 세 번 ACK 받은 세그먼트를 뒤따르는 세그먼트가 손실되었다는 신호
    - 세 번의 중복 ACK을 수신한 경우, TCP 송신자는 빠른 재전송 → 해당 세그먼트의 타이머가 만료되기 전에 손실된 세그먼트를 재전송

### **3.5.6 TCP Connection Management**

### [TCP(Transmission Control Protocol)]

- 인터넷상에서 데이터를 메세지의 형태로 보내기 위해 IP와 함께 사용하는 전송 프로토콜
- TCP는 애플리케이션에게 **신뢰적이고 연결지향성** 서비스를 제공
- 일반적으로 TCP와 IP는 함께 사용되며 IP: 전송, TCP: 패킷의 추적 및 관리
- TCP는 handshaking을 통해 신뢰적인 전송을 보장하고 데이터의 흐름제어와 혼잡제어를 수행
    - **속도는 느림**

---

### [3-way Handshake (접속)]

- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정하는 과정
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었음을 확인
- 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정

![image](https://github.com/user-attachments/assets/1ce284be-07a1-499b-85ec-47bf849e1b96)

![image](https://github.com/user-attachments/assets/59ff4b4d-260e-4165-8e7f-874fb38e928e)


1. Client -> Server : **SYN** 패킷 전송
    - **Client : SYN_SENT**
    - **Server : Wait for Client**
2. Server -> Client : **ACK, SYN** 패킷 전송
    - Client : SYN_SENT
    - **Server : SYN_RECEIVED**
        - **세그먼트 헤더 정보**
            - SYN 비트가 1로 설정됩니다.
            - TCP 세그먼트 헤더의 확인 필드가 client_isn+1로 설정
            - 서버는 자체 초기 시퀀스 번호(server_isn)를 선택, TCP 세그먼트 헤더 설정
3. Client -> Server : **ACK** 패킷 전송
    - **Client : ESTABLISHED**
    - **Server : ESTABLISHED**
- **`SYN(Synchronization)`** : 연결 확인을 위해 보내는 무작위 숫자값
- **`ACK(Acknowledgement)`** : Client 혹은 Server로부터 받은 SYN에 1을 더해 SYN을 잘 받았음을 알림
- 3번의 세그먼트 교환이 이뤄지지 않으면, 메시지를 전송하지 않음

---

### [4-Way Handshake(연결 해제)]

- 연결을 해제 (Connecntion Termination)하는 과정

![image](https://github.com/user-attachments/assets/8e8b5167-a9e9-498a-961a-ee203fbb085e)

1. Client -> Server : **FIN** 패킷 전송
    - **Client : FIN_WAIT**
    - **Server : ESTABLISHED**
2. Server -> Client : **ACK** 패킷 전송
    - Client : FIN_WAIT
    - **Server : CLOSE_WAIT** (자신의 데이터 전송이 끝날 때까지 기다림)
3. Server -> Client : **FIN** 패킷 전송 (서버 전송 끝나면)
    - Client : FIN_WAIT
    - **Server : LAST_ACK**
4. Client -> Server : **ACK** 패킷 전송
    - **Client : TIME-WAIT** -> 세션 만료 후 **CLOSE**
    - **Server : ESTABLISHED**
- **`FIN (finish)`** : 세션을 종료시키는데 사용되며, 더 이상 보낼 데이터가 없음을 나타냄

- Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 라우터 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생한다면?
    - **TIME_WAIT**: 이러한 현상에 대비하여 Client는 Server로부터 FIN 플래그를 수신하더라도 일정 시간동안 세션을 남겨 놓고 잉여 패킷을 기다림
- 초기 Sequence Number인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유?
    - 서버는 패킷의 SYN을 보고 패킷을 구분 -> 난수가 아닌 순처적인 Number가 전송된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수 있음

---

### [TCP VS UDP]

![image](https://github.com/user-attachments/assets/ee2f2321-afb8-426e-b5cd-ae824f941770)

## **3.6 Principles of Congestion Control**

### [흐름 제어]

> 송신측과 수신측의 **데이터 처리 속도 차이를 해결**하기 위한 기법
> 
- 송신 측의 속도가 수신측보다 빠를 경우, 수신 측에서 제한된 저장 용량을 초과한 이후에 도착하는 패킷은 손실될 수 있음
    - 만약 손실된다면 불필요한 추가 패킷 전송이 발생
- 송신 측과 수신 측의 TCP 버퍼 크기 차이로 인해 생기는 데이터 처리 속도 차이를 해결하기 위한 기법
- TCP 버퍼

<aside>
💡 송신 측- 버퍼에 TCP 세그먼트를 보관한 후 순차적으로 전송

수신 측- 도착한 TCP 세그먼트를 애플리케이션이 읽을 때까지 버퍼에 보관

</aside>

### 1. Stop and Wait

![image](https://github.com/user-attachments/assets/8f610445-9de8-41a2-b620-68b4c637baae)

- 매번 전송한 패킷에 대해 확인 응답(ACK)를 받으면 다음 패킷을 전송하는 방법
- 패킷을 하나씩 보내기 때문에 비효율적인 방법

### 2. Sliding Window

![image](https://github.com/user-attachments/assets/d76e8c87-530a-4042-9311-464e8bc1d41c)

![image](https://github.com/user-attachments/assets/3ecd6990-2e13-4700-a3dd-42dcc6a4ce1a)

- 수신 측에서 설정한 윈도우 크기만큼 송신 측에서 확인 응답(ACK) 없이 패킷을 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 제어 기법
- 윈도우에 포함된 패킷을 계속 전송하고, 수신 측으로부터 확인 응답(ACK)이 오면 윈도우를 옆으로 옮겨 다음 패킷들을 전송
- 윈도우 크기: '3 way handshaking'을 통해 수신 측 윈도우 크기로 설정되며, 이후 수신 측의 버퍼에 남아있는 공간에 따라 변함
    - 수신 측에서 송신 측으로 확인 응답(ACK)을 보낼 때 TCP 헤더(window size)에 담아서 보냄
- 재전송 : 송신 측은 일정 시간 동안 수신 측으로부터 확인 응답(ACK)을 받지 못하면, 패킷을 재전송함
- 재전송을 했는데, 패킷이 소실된 경우가 아니라 수신 측의 버퍼에 남는 공간 없는 경우?
    - 이를 해결하기 위해 수신 측은 해결 응답(ACK)을 보내면서 남은 버퍼의 크기(윈도우 크기)도 함께 보냄
- A가 보낸 미확인 데이터의 양이 rwnd의 값보다 작도록 유지
    
    → 호스트 A는 호스트 B의 수신 버퍼를 넘치게 하지 않도록 보장
    
    **`LastByteSent−LastByteAcked ≤ rwnd`**
    

---

### [혼잡 제어]

> 송신측의 데이터 전달과 네트워크 **데이터 처리 속도 차이를 해결**하기 위한 기법
> 
- 데이터의 양이 라우터가 처리할 수 있는 양을 초과하면 초과된 데이터는 라우터가 처리하지 못함
- 이때 송신 측에서는 라우터가 처리하지 못한 데이터를 손실 데이터로 간주하고 계속 재전송하여 네트워크를 혼잡하게 함
- **송신 측의 전송 속도를 조절**하여 예방할 수 있음

### 1. AIMD(Additive Increse/Multicative Decrease)

![image](https://github.com/user-attachments/assets/06a02330-73d1-40b8-a0e4-230df59da821)

- 합 증가/곱 감소 방식
- 처음에 패킷을 하나씩 보내고 문제 없이 도착하면 윈도우의 크기를 1씩 증가시켜가며 전송
- 전송에 실패하면 윈도우 크기를 반으로 줄임
- **단점**
    - 윈도우 크기를 너무 조금씩 늘리기 때문에 네트워크의 모든 대역을 활용하여 제대로 된 속도로 통신하기까지 시간이 오래 걸림

### 2. Slow Start (느린 시작)

- AIMD 방식과 달리 윈도우의 크기를 1, 2, 4, 8, ...과 같이 지수적으로 증가시키다가 혼잡이 감지되면 윈도우 크기를 1로 줄이는 방식
- **장점**
    - 보낸 데이터의 ACK가 도착할 때마다 윈도우 크기를 증가시키기 때문에 처음에는 윈도우 크기가 조금 느리게 증가하더라도, 시간이 지날수록 윈도우 크기가 점점 빠르게 증가

### 3. 빠른 재전송

- 패킷을 받는 수신자에게 세그먼트로 분할된 내용들이 순서대로 도착하지 않는 경우?
    - 수신 측에서는 순서대로 잘 도착한 마지막 패킷의 다음 순번을 ACK 패킷에 실어서 보냄
    - 중복 ACK를 3개 받으면 재전송이 이루어짐
- **장점**
    - 송신 측은 자신이 설정한 타임 아웃 시간이 지나지 않았어도 바로 해당 패킷을 재전송할 수 있기 때문에 보다 빠른 재전송률을 유지할 수 있음

### 4. 빠른 회복

- 혼잡한 상태가 되면 윈도우 크기를 1로 줄이지 않고 반으로 줄이고 선형 증가시키는 방법
- 혼잡 상황을 한 번 겪고나서부터는 AIMD 방식으로 동작함

### **3.6.1 The Causes and the Costs of Congestion 261**

-skip

### **3.6.2 Approaches to Congestion Control 268**

- 네트워크 혼잡 원인
    - 높은 전송률로 데이터를 전송하려는 너무나 많은 출발지-> 네트워크 혼잡을 일으키는 송신자를 억제하는 메커니즘 필요

### 종단 간 혼잡 제어

- TCP는 혼잡 제어를 위한 종단 간 접근 방식을 취합니다. 이는 IP 계층이 네트워크 혼잡에 대한 피드백을 호스트에 제공할 필요가 없기 때문입니다. TCP 세그먼트 손실(타임아웃이나 세 개의 중복된 확인 수신으로 표시됨)은 네트워크 혼잡의 징후로 간주되며, TCP는 창 크기를 줄임

### 네트워크 지원 혼잡 제어

- 라우터가 네트워크의 혼잡 상태에 대해 명시적인 피드백을 발신자 및/또는 수신자에게 제공합니다. 이러한 피드백은 링크의 혼잡을 나타내는 단일 비트와 같이 간단할 수 있습니다.
- 인터넷 기본 IP와 TCP 버전은 혼잡 제어를 위한 종단 간 접근 방식을 채택

### **3.7 TCP Congestion Control 269**

**혼잡 윈도우**(congestion window : cwnd) : TCP 송신자가 네트워크로 트래픽을 전송할 수 있는 비율을 제한

![image](https://github.com/user-attachments/assets/2a69e9e6-eb2f-438b-9a74-79d94b87efc6)
