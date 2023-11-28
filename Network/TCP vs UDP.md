## Prerequisite

### OSI 7: Transport Layer

[##_Image|kage@b1YP9F/btsA7CB5HF6/h1gxAPL2x87kF1zI0AsGw0/img.png|CDM|1.3|{"originWidth":623,"originHeight":313,"style":"alignCenter","caption":"OSI 7계층"}_##]

Transport Layer : OSI 7계층의 4 Layer로, 송신자와 수신자를 연결하는 통신 서비스를 제공하는 계층이다.

Transport Layer는 양 끝단 사용자들이 신뢰성 있는 데이터를 주고 받을 수 있게 한다.

Transport Layer는 TCP/IP Protocle과 OSI 모두 포함하고 있는 계층이다.

Transport Layer : Application 프로세스들 간 논리적 통신

Network Layer : host 간 논리적 통신을 제공

오늘 알아볼 **TCP**와 **UDP**는 모두 OSI 7 계층 중, Transport Layer에서 사용되는 프로토콜

  
  

## TCP (Transmission Control Protocol)

인터넷 상에서 **데이터를 메세지 형태로 전송**하기 위해 IP와 함께 사용하는 **연결형 프로토콜** (규약)

TCP는 애플리케이션에게 신뢰적이고 연결 지향성 서비스를 제공한다.

일반적으로 TCP와 IP는 TCP/IP 라는 이름으로 같이 사용된다.

IP는 데이터 배달을 담당하며, TCP는 패킷의 추적 및 관리를 수행한다.

TCP는 신뢰적 전송을 위한 handshaking 과정이 필요하고, 데이터의 흐름 제어와 혼잡 제어 과정이 필요하다.

-   흐름 제어 : 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지
-   혼잡 제어 : 네트워크 내 패킷 수가 과도하게 증가하는 것을 방지

따라서, 데이터를 신뢰성 있게 순서대로 에러 없이 교환할 수 있다.

대신 TCP의 수행 속도는 다소 느리다.

파일 전송과 같은 곳에 사용되기에 좋다.

  
  

### TCP의 특징

1\. 3-Way Handshake를 통해 연결을 설정하고, 4-Way Handshake를 통해 연결을 해제한다.

2\. 흐름 제어 및 혼잡 제어를 수행한다.

3\. 높은 신뢰성을 보장한다.

4\. UDP 보다 속도가 느리다.

5\. Full-Duplex(전이중), Point to Point(점대점) 방식

-   Full-Duplex : 전송이 양방향으로 발생할 수 있음
-   Point to Point : 각 연결이 정확히 2개의 종단점을 가짐

  
  

## UDP (User Data Protocol)

UDP : 데이터를 **Datagram** 단위로 서로 다른 경로로 독립 처리하는 **비연결형** **프로토콜**

**Datagram(데이터그램)** : 독립적인 관계를 지니는 패킷

비 연결형 프로토콜이기에, 각각 할당되는 논리적 경로가 있는 것이 아니라, 각 패킷이 다른 경로로 전송되며 독립적이다.

UDP는 비연결형 프로토콜이기 때문에, 연결을 설정하고 해제하는 과정이 필요 없다.

흐름 제어 및 혼잡 제어가 필요 없기 때문에 수행 속도가 빠르고 네트워크 부하가 적다.

그렇지만, 그러한 과정들이 없기 때문에 신뢰성이 낮다.

연속성이 중요한 실시간 스트리밍 서비스에 사용되기 좋다.

  
  

### UDP 특징

1\. 비연결형 서비스로 데이터그램 방식을 제공한다.

2\. 정보를 주고 받을 때, 신호 절차가 없다.

3\. UDP Header의 CheckSum Field를 통해 최소한의 오류만 검출

4\. 낮은 신뢰성

5\. TCP보다 속도가 빠르다.

  
  

## TCP vs UDP

UDP와 TCP는 각각 별도의 포트 주소 공간을 관리하므로, 같은 포트 번호를 사용해도 무방하다.

**두 프로토콜에서 동일한 포트 번호를 할당해도 서로 다른 포트로 간주한다.**

| **프로토콜 종류** | **TCP** | **UDP** |
| --- | --- | --- |
| **연결 방식** | 연결형 서비스 | 비연결형 서비스 |
| **패킷 교환 방식** | 가상 회선 방식 | 데이터그램 방식 |
| **전송 순서** | 전송 순서 보장 | 전송 순서 보장 X |
| **수신 여부 확인** | 수신 여부 확인 | 수신 여부 확인 X |
| **통신 방식** | 1:1 | 1:1 / 1:N / N:N |
| **신뢰성** | 높다 | 낮다 |
| **속도** | 느리다 | 빠르다 |

  
  

## 출처

\[\[네트워크\] TCP/UDP와 3 -Way Handshake & 4 -Way Handshake

TCP / UDP / 3-Way Handshake / 4-Way Handshake

velog.io\]([https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake#tcp-transmission-control-protocol](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake#tcp-transmission-control-protocol))
