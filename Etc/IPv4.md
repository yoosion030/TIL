# IPv4

IP는 Internet Protocol의 약자로 기기간 네트워크 통신 할 때 쓰는 프로토콜을 의미한다. IP에서 IP기기의 주소를 나타내는 것이 바로 IP 주소이다.
(집주소 같은 걸 의미한다.)

IP주소를 사용하는 이유는 각각의 host들을 구분하여 데이터를 정확하게 송수신 하기 위해서이다.

IPv4는 3자리 숫자가 4마디로 표기되는 방식이다. 각 마디는 옥텟이라고 부른다. 위 주소는 내부적으로 32비트로 처리되고 2진수로 처리하지만 사람이 보기 쉽게 10진수로 표기한다. (보이는건 10진수 이지만 처리할 때는 2진수로 처리한다는 것을 잊지말자!)

IPv4는 한 마디당 256개의 수를 나타낼 수 있어 `256^4 = 4,294,967,296`개의 주소를 만들 수 있다. 약 42억 개의 IP를 각각의 컴퓨터에 할당할 수 있는 것이다. 하지만 인터넷 환경이 발달함에 따라 어마어마하게 많은 수의 IP주소가 필요해져 새로운 주소 체계인 IPv6가 나오게 되었다.

## NetworkID HostID

하나의 IP주소에는 **Network ID**와 **Host ID**가 존재하고 있습니다.

먼저, Network ID는 **인터넷 상에서 모든 Host들을 전부 관리하기 힘들기에 한 Network의 범위를 지정하여 관리하기 쉽게 만들어 낸 것**입니다. 그리고 Host ID는 **호스트들을 개별적으로 관리하기 위해 사용하게 된 것**입니다.

따라서 우리가 인터넷을 사용할 때 Routing으로 목적지를 알아내고 찾아가는 등의 역할을 할 때에는 **NetworkID와 HostID가 합쳐진 IP주소**를 보게 됩니다.

홍대리는 집에 장롱이 필요하여 가구회사에 주문을 하였습니다.
장롱을 가져다 주는 배달원은 주소를 보고 홍대리의 집이 부산광역시 해운대구 우동 792번지라는걸 확인하고 도착하였습니다. 그런데 배달원은 집까지 가져왔지만 어느 곳에 두어야 할 지 모릅니다. 이 때 홍대리가 작은 방의 한쪽 구석을 가리키며 정확한 위치를 알려주었습니다.

이 예시를 보면 배달원의 역할은 최종 목적지가 속한 지역(집)까지 전달하는 Network ID에 해당합니다. 그리고 홍대리는 자신의 지역(집)에서 최종적으로 장롱을 두어야 하는 위치를 안내하여 주기에 Host ID의 역할로 보시면 되겠습니다.

## 클래스

IP주소는 대역에 따라 A, B, C, D, E 클래스로 나뉜다. 이 클래스들을 구분함으로써 클래스 내에서 NetworkID와 HostID를 구분하게 된다.

- A Class : **대규모 네트워크 환경**에 쓰이며, 첫번째 마디의 숫자가 `0~127`까지 사용된다. (ex : 12.123.123.123)
- B Class : **중규모 네트워크 환경**에 쓰이며, 첫번째 마디의 숫자가 `128~191`까지 사용된다. (ex : 128.123.123.123)
- C Class : **소규모 네트워크 환경**에 쓰이며, 첫번째 마디의 숫자가 `192~223`까지 사용된다. (ex : 192.168.0.1)
- D Class : 멀티캐스팅용으로 쓰인다. 잘 쓰이지 않는다.
- E Class : 연구/개발용 혹은 미래에 사용하기 위해 남겨놓은 클래스로 일반적인 용도로 사용되지 않는다.

### A Class

A 클래스는 하나의 네트워크가 가질 수 있는 호스트 수가 가장 많은 클래스이다. 네트워크 영역은 8비트 호스트 영역은 24비트로 이루어져 있다.

첫 번째 옥텟의 범위는 `0~127`이고 1개의 네트워크 영역이 각각 가질 수 있는 호스트 ID는 **(2^24) - 2** 개이다.
**2개를 제외하는 이유는 시작 주소인 x.0.0.0은 네트워크 주소로 사용하고 마지막 주소인 x.255.255.255는 브로드캐스트 주소로 사용하기 때문이다.**

### B Class

B 클래스의 네트워크 영역은 16비트 호스트 영역은 16비트로 이루어져 있다.

첫 번째 옥텟의 범위는 `128~191`이고 1개의 네트워크 영역이 각각 가질 수 있는 호스트 ID는 **(2^16) - 2** 개 이다.

### C Class

C 클래스의 네트워크 영역은 24비트 호스트 영역은 8비트로 이루어져 있다.

첫 번째 옥텟의 범위는 `192~223`이고 1개의 네트워크 영역이 각각 가질 수 있는 호스트 ID는 **(2^8) - 2** 개 이다.

## 예시

아래의 IP주소를 보고 클래스, 네트워크 영역, 호스트 영역을 구분해보자.

P1) 132.12.11.4

클래스 : B

네트워크 영역 : 132.12.0.0

호스트 영역 : 11.4
