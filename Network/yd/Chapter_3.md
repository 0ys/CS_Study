# 3.1 트랜스포트 계층 서비스 및 개요

- 트랜스포트 계층 프로토콜은 애플리케이션 프로세스 간의 **논리적 통신**을 제공
- 논리적 통신은 애플리케이션 관점에서 보면 프로세스들이 동작하는 **호스트들이 직접 연결된 것처럼** 보인다는 것을 의미함
- 트랜스포트 계층 프로토콜은 종단 시스템에서 구현된다.
- 애플리케이션 메시지를 작은 조각으로 분할하고, 각각에 헤더를 추가함으로써 **메시지를 세그먼트로 변환한다. → 네트워크 계층으로 세그먼트 전달**
- 트랜스포트 계층 프로토콜
    - TCP, UDP

## 3.1.1 트랜스포트 계층과 네트워크 계층 사이의 관계

- 트랜스포트 계층 프로토콜은 호스트에서 동작하는 **프로세스들 사이의 논리적 통신**을 제공
- 네트워크 계층 프로토콜은 **호스트들 사이의 논리적 통신**을 제공

## 3.1.2  인터넷 트랜스포트 계층의 개요

- 비신뢰적이고 비연결형 서비스
    - UDP, 무결성 검사 제공, 트래픽은 조절되지 않음.
- 신뢰적이고 연결지향형 서비스
    - TCP, 무결성 검사 제공, 혼잡제어
- 네트워크 계층 프로토콜
    - IP
    - IP는 세그먼트의 전달을 보장하지 않고 세그먼트가 순서대로 전달되는 것을 보장하지 않음
    - IP는 비신뢰적인 서비스

# 3.2 다중화와 역다중화

- 소켓
    - 애플리케이션과 트랜스포트 사이에 존재
    - 네트워크 애플리케이션의 한 부분으로서 프로세스가 갖고 있다.
    - 수신 측 호스트의 트랜스포트 계층은 직접 데이터를 프로세스로 전달하지 않고 **중간 매개자인 소켓에게 전달한다.**
    - 하나 이상의 소켓이 있을 수 있으므로, **각각의 소켓은 하나의 유일한 식별자를 가짐**
        - 식별자 포맷은 UDP 소켓, TCP 소켓인지에 따라 달라짐
- 역다중화
    - 트랜스포트 계층 세그먼트의 데이터를 올바른 소켓으로 전달하는 작업
- 다중화
    - 출발지 호스트에서 소켓으로부터 데이터를 모으고, 이에 대한 세그먼트를 생성하기 위해 헤더 정보를 추가해 캡슐화 → 그 세그먼트들을 네트워크 계층으로 전달하는 과정
- 각 세그먼트는 세그먼트가 전달된 적절한 소켓을 가르키는 특별한 필드를 가짐
    - **출발지 포트 번호 필드**, **목적지 포트 번호 필드**

## 비연결형 다중화와 역다중화

- UDP 소켓
    - 목적지 IP 주소와 목적지 포트 번호로 구성된 두 요소로 된 집합에 의해 식별된다.
    - 같은 목적지 IP 주소와 목적지 포트 번호를 가지면 2개의 세그먼트는 같은 목적지 소켓을 통해 같은 프로세스로 향한다.

## 연결지향형 다중화와 역다중화

- TCP 소켓
    - 출발지 IP 주소, 출발지 포트 번호, 목적지 IP 주소, 목적지 포트 번호에 의해 식별된다.
    - UDP와는 달리 다른 출발지 주소 또는 다른 출발지 포트 번호를 가지고 도착하는 2개의 TCP 세그먼트는 2개의 다른 소켓으로 향하게 된다.

# 3.3 비연결형 트랜스포트: UDP

- UDP는 트랜스포트 계층 프로토콜이 할 수 있는 최소 기능으로 동작
- 핸드셰이크를 사용하지 않는다.
- DNS는 전형적인 UDP를 사용하는 애플리케이션 계층 프로토콜
- 아래와 같은 이유로 TCP보다 UDP를 선호한다.
    - 무슨 데이터를 언제 보낼지에 대해 애플리케이션 레벨에서 더 정교한 제어
        - TCP는 신뢰적인 전달이 얼마나 오래 걸리는지 관계 없이 목적지가 세그먼트 수신 여부를 응답할 때까지 데이터의 세그먼트 재전송을 계속한다.
        - 조금의 데이터 손실은 허용하는 곳에서 적합하지 않음
    - 연결 설정이 없음
        - TCP는 세 방향 핸드셰이크를 위한 지연 발생
        - UDP는 그러한 연결 설정을 위한 지연이 없음
    - 연결 상태가 없음
        - TCP에서 연결 상태는 수신 버퍼와 송신 버퍼, 혼잡 제어 파라미터, 순서 번호와 확인응답 번호 파라미터를 포함. UDP는 그런 거 없음
    - 작은 패킷 오버헤드
        - TCP는 세그먼트마다 20바이트의 오버헤드, UDP는 단지 8바이트의 오버헤드
- 초기 HTTP는 TCP를 통해 실행
- 최신 HTTP는 UDP를 통해 실행 → 애플리케이션 계층에서 자체 오류 제어 및 혼잡 제어 제공
- UDP를 사용할 때도 신뢰적인 데이터 전송이 가능. 신뢰성을 애플리케이션 자체에서 제공한다면 신뢰적인 데이터 전송을 할 수 있다.

## 3.3.1 UDP 세그먼트 구조

- 포트 번호
    - 목적지 호스트가 목적지 종단 시스템에서 동작하는 정확한 프로세스에게 애플리케이션 데이터를 넘기게 해준다.
- 체크섬
    - 세그먼트에 오류가 발생했는지를 검사하기 위해 수신 호스트가 사용

## 3.3.2 UPD 체크섬

- 체크섬은 세그먼트가 출발지로부터 목적지로 이동했을 때 UDP 세그먼트 안의 비트에 대한 변경 사항이 있는지 검사하는 것
- 체크섬 제공 이유
    - 출발지와 목적지 사이의 모든 링크가 오류 검사를 제공한다는 보장이 없기 때문
    - 세그먼트가 라우터의 메모리에 저장될 때 비트 오류가 발생할 수도 있기 때문
- UDP는 오류 검사는 제공하지만, 오류 회복을 위한 어떤 일도 하지 않음

# 3.4 신뢰적인 데이터 전송의 원리

- 신뢰적인 채널에서는 전송된 데이터가 손상되거나 손실되지 않는다.
- 모든 데이터는 전송된 순서 그대로 전달된다.
- 이것이 TCP
- 이 작업은 신뢰적인 전송 프로토콜의 ‘아래에 있는’ 계층이 신뢰적이지 않을 수 있어 어려워진다.

## 3.4.1 신뢰적인 데이터 전송 프로토콜의 구축

### 비트 오류가 있는 채널상에서의 신뢰적 데이터 전송: rdt2.0

- 메시지 수신자는 문장 수신 → “OK” 또는 반복 요청
- 이러한 메시지 받아쓰기 프로토콜은 긍정 확인응답(”OK”)과 부정 확인응답(”그것을 반복해주세요”) 둘 다 사용
- 컴네에서 그러한 재전송을 기반으로 하는 신뢰적 데이터 전송 프로토콜은 **자동 재전송 요구(ARQ) 프로토콜**로 알려져있다.
- ARQ 프로토콜에 요구되는 것
    - 오류 검출: 비트 오류가 발생했을 때 수신자가 검출할 수 있는 기능
    - 수신자 피드백: 수신자가 송신자에게 피드백 제공. 긍정 확인응답(ACK), 부정 확인응답(NAK)
    - 재전송: 수신자에서 오류를 가지고 수신된 패킷은 송신자에 의해 재전송 됨.
- 이 프로토콜은 **전송 후 대기(stop-and-wait) 프로토콜**로 알려져 있음.
- 손상된 ACK 또는 NAK 처리 방법
    - 중복 패킷 전송
    - 데이터 패킷에 새로운 필드를 추가 → 필드 안에 순서 번호 삽입. 데이터 패킷에 송신자가 번호를 붙임.
    - 수신자는 수신된 패킷이 재전송인지를 결정할 때에는 이 순서 번호만 확인하면 됨.

### 비트 오류와 손실 있는 채널상에서의 신회적인 데이터 전송: rdt3.0

- 패킷을 손실할 경우
- 송신자가 어떤 패킷을 손실했다는 것을 확신하기 위해 얼마나 오랫동안 기다려야 할지 알 수 없음
- 따라서 일정 시간을 정하고 이 시간 안에 ACK가 수신되지 않았다면 패킷을 재전송한다.

## 3.4.2 파이프라이닝된 신뢰적인 데이터 전송 프로토콜

- rdt 3.0은 기능적으로 좋지만 고속 네트워크에서 성능은 좋지 않다.
- rdt 3.0이 전송 후 대기(stop-and-wait) 프로토콜이기 때문
- 해결법
    - 전송 후 대기 방식으로 동작하는 대신 송신자에게 확인 응답을 기다리지 않고 여러 패킷을 전송하도록 허용한다.