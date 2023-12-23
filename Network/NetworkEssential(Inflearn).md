## 외워서 끝내는 네트워크 핵심이론

### MAC, IP, Port
- **MAC** : L2 layer, 랜카드 식별자
- **IP** : L3 Layer, Host 식별자
- **Port** : L4 Layer, Process & L2 Interface & Network Service 식별자

### Host
호스트는 네트워크에 연결된 장치(컴퓨터)를 의미한다. 그리고 이 장치의 목적에 따라 또 두가지로 구분할 수 있다.
- Switch : 스위치나 라우터 등 네트워크 그 자체를 이루는 장치
- End-Point : 클라이언트, 서버 등 서비스를 구성하는 단말 장치

### Swith가 하는 일
스위치는 고속도로망에 비유했을 때, 매 교차로마다 어디로 가는 것이 더 효율적일지 판단하는 장치라고 할 수 있다.
- **Router** : L3 Switch라고도 하며, 목적지까지 가기위한 경로를 판단하는 스위치이다.
- **Routing table** : 고속도로 상의 이정표와 같은 역할을 하는 테이블. 라우터는 라우팅 테이블을 기준으로 경로를 선정한다.
- **Packet** : 네트워크망을 통해 이동하는 데이터의 단위
- **Metric** : 라우팅 테이블에서 각각의 목적지로 이동하는 비용의 개념. 라우터는 가장 적은 비용의 경로를 선택한다.
  
### L2 Layer 용어들

- **NIC(Network Interface Card)** : == LAN(Local Area Network) Card와 동일한 의미
- **L2 Frame** : Ethernet Frame이라고도 하며, 2계층 네트워크에서 데이터를 전송할 때 사용되는 기본 단위이다.
- **L2 Access Switch** : End-point(NIC)와 직접적으로 연결되는 스위치. MAC Adress를 기반으로 스위칭 한다.
  - Link-up & Link-down : L2 스위치 포트의 상태를 의미하는 용어. link-up은 정상 연결 상태를, link-down은 단절 상태를 의미한다.
  - *Uplink : 상위 네트워크로 연결되는 것을 의미하는 용어. L2와 별개로 네트워크 장비의 계층구조를 표현할 때 쓰인다.
- **L2 Distribution Switch** : L2 Access 스위치를 위한 스위치. VLAN(Virtual LAN)을 제공하기위해 사용하는 것이 일반적.
- **Broadcast** : 1:1 단방향 네트워크 통신이 아닌 1:N 전방향 네트워크 통신을 의미한다. 네트워크에는 broadcast 통신을 위한 특별한 주소가 있다. Frame header에 오는 목적지 주소는 48bit의 MAC주소가 입력되는데, 이 주소가 모두 1로 이루어져 있으면 이는 특정 NIC가 아닌 전체 네트워크에 전송한다는 뜻이다.
  - broadcast의 문제점 : 브로드캐스트 통신의 문제점은 해당 통신이 전송되는 순간 모든 네트워크는 해당 브로드캐스트 통신을 처리하느라 다른 네트워크 통신이 지연되게 된다. 이 문제 때문에 네트워크는 단순히 모든 네트워크에 브로드 캐스팅을 하는 게 아닌 특정 규칙에 따라 전송하는데, 이를 어떻게 전송할 것인가에 대한 부분은 상당히 복잡한 문제이다.
- **LAN과 WAN** : 일반적으로 LAN은 2계층 이하의 통신을 의미하는데, 이는 달리 말하면 물리적인 계층이라 할 수 있다. WAN(Wide Area Network)는 일반적으로 인터넷을 의미하고, 이는 물리가 아닌 논리적 네트워크 또는 가상화 네트워크라고 부른다.

### L3 Layer 용어들
- **IPv4** : 32비트 IP 주소체계. dot으로 구분하며 각 자리에는 8비트의 수가 올 수 있다. 주로 앞쪽 3자리 까지는 네트워크 주소를 의미하며, 마지막은 호스트 주소를 의미한다.
- **Packet** : L3 IP(Internet Protocol)에서의 데이터 단위이다. src/dest를 포함하는 헤더와 페이로드 데이터로 구성되어 있다.
- **MTU(Maximum Transmission Unit)** : 패킷의 최대 크기. 1500byte 로 약 1.4KB 이다.
- **Wireshark** : 네트워크 도/감청 프로그램. 패킷의 상세 정보를 확인할 수 있다.
- **En/Decapsulation** : 캡슐화/역캡슐화로, 네트워크 데이터를 각 레이어의 형식에 맞게 포장하고 해제하는 것을 의미한다. 네트워크 데이터는 여러 층의 중첩 캡슐화로 구성되어 있다.
  * **네트워크 데이터 구조**
  ![img.png](../assets/network_data_structure.png)  
- #### 네트워크 계층별 데이터 단위
  - Stream : 5~7계층 데이터의 단위. header/payload 구조가 아닌 직렬화된 형태를 지닌다.
  - Segmentation : 4계층 TCP의 데이터 단위. MSS(Maximum Segment Size)는 1460byte이다.
  - Packet : 3계층 IP의 데이터 단위.
  - Frame : 1~2계층 데이터의 단위