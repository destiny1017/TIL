## 네트워크 관련 개념들

### URL / URI
- **URL(Uniform Resource Locator)**
    - 리소스 위치를 나타내는 주소로, https://www.naver.com/ 과 같은 형식이다.
- **URI(Unifirm Resoutce Indentifier)**
    - 리소스의 식별자로, 페이지에 나타내고자 하는 데이터를 결정하는 parameter를 포함한 url이라고 생각하면 된다.
        - ex) https://mail.naver.com/read/1383 → 1383은 read페이지에서 읽고자 하는 메일의 코드이므로 URI에 해당
        - ex) [https://search.naver.com/search.naver?query=검색어](https://search.naver.com/search.naver?query=%EA%B2%80%EC%83%89%EC%96%B4)  query=검색어 queryParam은 search.naver페이지에서 나타낼 데이터 식별자를 뜻하므로 URI에 해당

### TTL(Time To Live)
- IP패킷 내부에 있는 값으로, 해당 패킷이 네트워크에 너무 오래있어 버려야하는지 여부를 알려주는 역할
- 부정확한 라우팅 결합으로인해 패킷이 끝없이 순환하는 현상을 방지해준다.
- 라우터를 거칠 때마다 1씩 TTL값이 감소하고, 0이하로 떨어지면 라우터는 더이상 패킷을 보내지 않고 폐기한다.

### CDN(Content Delivery Network)
- 전세계에 네트워크를 분산시켜 정적인 요소들을 복사해두고 클라이언트의 리소스 요청에 빠르게 응답해주는 네트워크
- 컨텐츠를 복사해둔 서버로 요청과 응답이 이루어지는 구조이므로 디도스 등의 서버 공격 대응에도 유리하다.
- CDN 자체는 라운드로빈 방식만 사용하므로 장애대응이 되지 않아 GSLB와 함께 활용하여 사용한다.

### SSE(Server Sent Event)
1. 실시간 단방향 통신을 위한 기술. 서버에서 클라이언트로의 전송만 가능하다.
2. 웹소캣에비해 리소스 사용량이 적다. 단, IE미지원, HTTP통신이용시 6개탭까지만 지원(http2는 100개)
3. 실시간이지만 웹소캣만큼 전송속도에 집착하지 않는다. 그래서 알람받기 기능 등에 주로 이용

### 브라우저 주소창에 [www.naver.com](http://www.naver.com) 입력 시 일어나는 일
- 입력한 주소가 IP가 아닌 도메인이므로 해당 도메인에 해당하는 IP를 획득하기 위해 아래의 과정을 거친다.
    1. 브라우저 실행중인 local PC의 hosts파일을 확인하여, 입력한 도메인과 매핑된 IP가 있는지 확인하여 있으면 IP반환
    2. hosts에 매핑데이터가 없으면, 이번에는 OS의 DNS캐시저장소를 확인함. 해당 도메인의 캐싱 데이터가 있으면 IP반환
    3. dns캐시도 없으면, 로컬 dns서버가 있는지 확인하여 로컬 dns서버에 dns질의를 전달하고 응답을 받아 IP반환
    4. 3번까지의 과정에서 모두 해당하지 않으면 dns 질의 설정에 따라 외부 DNS서버로 질의 전달.
        - 질의 설정은 커스텀 설정 값이 없으면 ISP에서 제공하는 기본 설정을 따른다.
        - 공유기 사용시 이 과정에서 DNS질의를 하는 요청자는 local pc가 아닌 공유기가 될 수도 있다.
- DNS서버에서 받아온 Naver Server IP로 TCP연결을 하여 HTTP Request 전송
- 서버 처리결과 response를 받아 응답 데이터에 따른 내용을 브라우저 상에 표시