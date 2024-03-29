# TCP와 UDP에 대해서 알아보자.

### `선 3줄 요약`

1. TCP와 UDP는 둘다 전송 계층에서 데이터를 보내기 위해 사용하는 프로토콜 입니다.
2. TCP는 연결형 서비스로 가상 회선 방식을 제공하고, 높은 신뢰성을 보장하고 흐름 제어 및 혼잡 제어 기능을 제공합니다.
3. UDP는 비연결형 서비스로 데이터그램 방식을 제공하고, 패킷에 순서 부여나 재조립등의 기능을 처리하지 않기 때문에 연속성이 중요한 서비스에 사용됩니다.

---

TCP와 UDP. 네트워크의 계층들 중 전송 계층에서 사용하는 프로토콜입니다.

전송계층은 송신자와 수신자를 연결하는 통신서비스를 제공하는 계층으로, 쉽게 말해 데이터의 전달을 담당합니다. 그리고 데이터를 보내기 위해 사용하는 프로토콜이 있는데, 그것들이 바로 TCP와 UDP 입니다.

## TCP(Transmission Control Protocol)

직해 : 전송을 제어하는 규약 인터넷상에서 데이터를 메시지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜

일반적으로 TCP와 IP를 함께 사용합니다.

IP : 데이터의 배달을 처리
TCP : 패킷을 추적 및 관리합니다.
TCP는 연결형 서비스를 지원하는 프로토콜로 인터넷 환경에서 기본으로 사용합니다.

![TCP의 특징](https://t1.daumcdn.net/cfile/tistory/991BEB3359FEB5712F)
