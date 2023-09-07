# 📖 OSI 7 계층

## 📌 OSI 7 계층이란?

- 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것

<br><br>

## 📌 왜 7 계층으로 나눠야 할까?

- 통신이 일어나는 과정이 꽤 복잡하다.
  - 이 복잡한 과정을 단계별로 파악하여 흐름을한눈에 보기 쉽고, 사람들이 이해하기 쉽다.
  - 특정 문제가 발생했을 때 다른 단계를 수정하지 않고도 이상이 생긴 단계만 수정하여 문제를 해결할 수 있다.

<br><br>

## 📌 OSI 7 계층에 대해 자세히 알아보자.

<br>

![img.png](img.png)

- OSI 7 계층은 위의 그림과 같이, 7단계의 계층들의 순서에 따라 각 계층에서 담당하는 기술과 방식으로 데이터를 종단에서 반대쪽 종단으로 전달한다.

<br>

### ✅ Layer 1 : Physical Layer(물리 계층)

![img_1.png](img_1.png)

> - 데이터를 전기적 신호로 변환하여 전송하는 계층

- 전기, 물리 신호에 대한 계층

<br>

- `Bit` 단위를 사용
  - 전기적 신호 (0 or 1)을 나타낼 때 사용하는 단위
  - 0과 1은 Off, On를 나타낸다.
  
<br>

- 단순 전기적 신호를 전달하는 역할
  - 오류 제어, 알고리즘 등이 없음.
    - 데이터가 무엇인지, 어떤 에러가 있는지는 전혀 신경쓰지 않는다.
    - 단지 데이터를 전기적 신호로 변환하여 주고 받기만 한다.

<br>

- 송신 : 2 계층(Data Link Layer)로부터 0, 1로 구성된 비트열 데이터(Frame)을 받아 전기적 신호로 변환 후 전송
- 수신 : 전기적 신호를 0, 1로 구성된 비트로 복원하여 2 계층(Data Link Layer)로 전송

<br>

- 통신 단위
  - 비트(Bit)

- 대표 장비 : 랜 케이블, 허브, 리피터, 전선, 광케이블, 동축케이블, 무선 전파, PSTN, DSU, CSU, 모뎀 등

<br><br>

### ✅ Layer 2 : Data Link Layer(데이터 링크 계층)

![img_2.png](img_2.png)

> - Physical Layer로 송수신되는 정보를 관리하여 안전하게 전달되도록 돕는 계층
> - Mac 주소를 통해 통신
> - Frame에 MAC 주소를 부여하고, 에러 검출 / 재전송 / 흐름 제어를 진행한다.

- 1계층(Physical Layer)을 통해 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행하도록 도와준다.
  - 과도한 양의 데이터가 한번에 전송되지 않도록, 데이터의 양을 조절한다.
  - 데이터의 오류를 검출하고 복구하는 오류 제어 / 흐름 제어를 수행한다.

<br>

- 1~3 계층에서는 논리 주소(ex> IP 주소)가 아닌 물리 주소(ex> MAC 주소)를 참조하여 각 장비별 데이터 전송을 수행한다.
  - - 1 계층(Physical Layer)에서 발생할 수 있는 오류를 찾고 수정하는데 필요한 기능 / 절차를 제공한다.

<br>

- Data Link Layer의 흐름
  - <span style="color:yellow">**물리적 주소**</span>를 지정한다. (ex> MAC 주소)
  - <span style="color:yellow">**전송 데이터(비트 모음)의 헤더에 목적지 주소**</span>를 붙인다.
  - <span style="color:yellow">**꼬리 부분에 오류 검출**</span>을 위한 부분이 존재한다.
  - 이 처럼 Data Link Layer에서 데이터를 <span style="color:red">**프레임(Frame)**</span>이라고 한다.
    - Data Link Layer의 데이터 단위 : 프레임(Frame)
  - 프레임의 구성요소
    - Header : MAC 주소 (물리적 주소)
    - Data : 4계층(Transport Layer)의 Header와 Packet
    - Trailer :  오류 검출을 위해 사용
      - FCS(Frame Check Sequence, 프레임 체크 문자열)
      - CRC(Cyclick Redundancy Check, 순환 중복 검사)

<br>

- 포인트 투 포인트(Point to Point)간 신뢰성 있는 전송을 보장하기 위해 CRC 기반 오류 제어와 흐름 제어가 필요하다.
  - 네트워크 위의 개체들 간 데이터를 전달
  - 1계층 (Physical Layer)에서 발생할 수 있는 오류를 찾고 수정하는데 필요한 기능적, 절차적 수단 제공


<br>

- Data Link Layer의 부계층
  - LLC(Logical Link Control, 논리적 연결 제어) : Data Link Layer의 기본 기능을 다룬다.
  - MAC(Media Access Control, 매체 접근 제어) : 물리적 전송 선로의 특징과 매체 간 연결 방식에 따른 제어 부분 처리

<br>

- 통신 단위
  - 프레임(Frame)

- 대표 장비
  - 브릿지, 스위치(L2 Switch) 등
- 대표 프로토콜 / 기술 
  - MAC(물리적 주소), PPP(Point to Point Protocol) 등

<br><br>

### ✅ Layer 3 : Network Layer(네트워크 계층)

![img_3.png](img_3.png)

> - 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능 담당
> - 라우터를 통해 이동할 경로를 선택하여 IP 주소를 지정하고, 해당 경로에 따라 패킷을 전달
> - 라우팅, 흐름 제어, 오류 제어, 세그먼테이션 수행

- 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능 (Routing, 라우팅)
- 경로를 선택하고 주소를 정하고 경로에 따라 패킷을 전달
- 다양한 길이의 데이터를 네트워크들을 통해 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 제공하기 위한 기능적, 절차적 수단 제공

<br>

- 데이터를 연결하는 다른 네트워크를 통해 전달함으로써 인터넷이 가능하게 만드는 계층
- IP(논리적 주소 구조, 네트워크 관리자가 직접 주소를 할당하는 구조), 계층적(hierarchical)
- 계층 사이에 네트워크 서비스 데이터 유닛(NSDU : Network Service Data Unit)을 교환하는 기능 제공

<br>

- 라우팅, 흐름 제어, 세그멘테이션, 오류 제어, 인터네트워킹 등 수행
  - 라우팅 : 패킷 전달을 위해 할당된 IP 주소를 기반으로 네트워크를 구분


<br>

- 통신 단위
  - 패킷(Packet)

- 대표 장비
  - 라우터, Layer3 스위치(IP 주소 사용)

<br><br>

### ✅ Layer 4 : Transport Layer(전송 계층)

![img_4.png](img_4.png)

> - TCP, UDP 프로토콜을 통해 통신을 활성화
> - 포트를 열고, 프로그램들이 전송할 수 있도록 제공

<br>

- 통신 단위
  - 세그먼트(Segment)

- 대표 장비
  - 게이트웨이
- 프로토콜
  - TCP : 연결성 데이터 전송 프로토콜
    - 데이터 전송 시 신뢰성 높은 데이터 전송
    - 3 Way-HandShaking 작업 수행
  - UDP : 비연결성 데이터 전송 프로토콜
    - 데이터 전송을 할 시 신뢰성이 낮은 대신 빠른 전송 제공

<br><br>

### ✅ Layer 5 : Session Layer(세션 계층)

> - 데이터가 통신하기 위한 논리적 연결 담당
> - TCP/IP 세션을 만들고 없애는 책임을 가짐

<br><br>

### ✅ Layer 6 : Presentation Layer(표현 계층)

> - 데이터 표현에 대한 독립성을 제공하고 암호화하는 역할을 담당
> - 파일 인코딩, 명령어를 포장, 압축, 암호화

<br><br>

### ✅ Layer 7 : Application Layer(응용 계층)

> - 최종 목적지로서, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스 수행
> - 사용자 인터페이스, 전자우편, DB 관리 등의 서비스 제공

<br><br>

## 📚 출처

- https://gyoogle.dev/blog/computer-science/network/OSI%207%EA%B3%84%EC%B8%B5.html
- https://shlee0882.tistory.com/110
- https://www.stevenjlee.net/2020/02/09/%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-osi-7%EA%B3%84%EC%B8%B5-%EA%B7%B8%EB%A6%AC%EA%B3%A0-tcp-ip-4%EA%B3%84%EC%B8%B5/
- https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kyg3766&logNo=220691506863
- https://m.blog.naver.com/kyg3766/220691524213

<br><br>