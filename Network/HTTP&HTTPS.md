### HTTP
- #### 특징
    1. Hyper Text Tranfer Protocol의 약자.
    2. OSI 7계층인 application계층 소속으로, 4계층인 TCP를 기반으로 통신한다고 생각하면 된다.(UDP로 통신할 수도 있긴함)
    3. Header와 Body(Payload)를 주고 받는 게 핵심
- #### HTTP 1.1
    1. 기본적으로 Connection당 하나의 요청을 처리
    2. HOL(Head Of Line) Blocking, RTT(Round Trip Time), Heavy Header문제가 있음

       → 참고(https://it-mesung.tistory.com/159)

- #### HTTP 2.0
    1. HTTP 1.1에서 성능과 속도를 향상시킨 버전
    2. Multiplexed Streams, Stream Prioritization, Server push, Header Compression을 사용, 성능향상
    3. 한 커넥션으로 여러 메시지 통신,  요청리소스간 우선순위 설정, 요청 없이 서버에서 응답 전송,  중복헤더 제거 및 인코딩


### HTTPS
- HTTP(HyperText Transfer Protocol)는 html을 전송하기위한 통신규약인데, HTTP전송시에는 일반적으로 전송데이터가 암호화되지 않아 외부에서 데이터를 파악하기가 쉽다.
- 이런 보안상의 문제를 해결하기위해 도입된 것이 SSL/TLS로, 이 기술이 적용된 사이트는 https프로토콜이 부여된다.
- #### SSL/TLS(Secure Soket Layer / Transport Layer Security)
    - 기본적으로 SSL과 TLS는 같은 의미로 사용되며, 정확히는 TLS가 SSL의 향상된 버전이나 보통은 다 SSL로 부른다.
    - SSL인증서란 서버와 클라이언트간의 통신을 제 3자가 보증해주는 문서이다.
    - 클라이언트가 서버에 접속 시 데이터 전송에 앞서 SSL HandShaking을 거친다. 이 과정은 클라이언트가 서버에 SSL인증서를 요청하여 서버가 인증서를 전달해주면, 클라이언트에서 신뢰할 수 있는 인증서인지 확인하는 과정이다.
    - SSL handshaking과정에서는 공개키/비밀키를 사용하여 인증서를 암/복호화한다.
    - 신뢰할 수 있는 인증서임이 확인된 후에는 클라이언트가 공개키로 pre master key를 생성하여 서버로 전송하고, 서버는 비밀키를 이용하여 복호화한다.
    - 복호화 하면 해당키를 master key로 사용하여 세션을 형성하고, 세션 유지 중에는 이 master key라는 대칭키로 데이터를 암호화한다.

참고 : https://goodgid.github.io/TLS-SSL/