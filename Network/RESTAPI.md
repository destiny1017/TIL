## REST API
- Representational State Transfer의 약자, 자원을 이름으로 구분하여 해당자원의 상태를 주고 받는 모든 것을 의미
- HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 자원에 대한 CRUD Operation을 적용하는 것을 의미
- #### 장점
    - HTTP 표준 프로토콜 인프라를 사용하여 별도의 API 인프라 구축을 요하지 않음
    - HTTP 요청의 내용이 의도하는 바를 명확하게 나타내어 이해가 쉽다
    - 서버와 클라이언트의 역할을 명확하게 분리한다
- #### 단점
    - 표준이 존재하지 않는다
    - method가 4가지 밖에 없어 형태가 제한적이다
    - 구형브라우저가 아직 제대로 지원해주지 못하는 부분이 존재
        - PUT, DELETE지원 미비 등
- #### REST 특징
    - Servler-Client 구조
    - Stateless
    - Cacheable
    - Layered System(계층화)
    - HASTEOAS
- #### REST API 설계 기본 규칙
  - URI는 자원의 정보를 표시해야 한다.
    - resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다
    - resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다
    - resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다
    - resource의 스토어 이름으로는 복수 명사를 사용해야 한다
      자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE) 로 표현한다.
    > GET /Member/1  -> GET /members/1

  - URI에 HTTML Method가 들어가면 안된다
    > GET /members/delete/1 -> DELETE /members/1  

  - URI에 행위에 대한 동사 표현이 들어가면 안된다(CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)
    > GET /members/show/1 -> GET /members/1  
      GET /members/insert/2 -> POST /members/2

  - 경로 부분 중 변하는 부분은 유일한 값으로 대체한다(즉 :id는 하나의 특정 resource를 나타내는 고유값이다)

    > Ex) student를 생성하는 route: POST/students  
      Ex) id=12인 student를 삭제하는 route: DELETE/students/12

- #### REST API 설계 규칙
  - 슬래시 구분자(/)는 계층 관계를 나타내는데 사용한다.
    > http://restapi.example.com/houses/apartments
  - URI 마지막 문자로 슬래시를 포함하지 않는다
  - URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르며 URI도 달라져야 한다.
    > http://restapi.example.com/houses/apartments/ (x)
  - 하이픈(-) 은 URI 가독성을 높이는데 사용
  - 불가피하게 긴 URI 경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
  - 밑줄(_)은 사용하지 않는다.
  - 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용 x
  - URI 경로에는 소문자가 적합
  - URI 경로에 대문자 사용은 피하도록 한다
  - RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
  - 파일 확장자는 URI에 포함하지 않는다.

- 참고 : https://hanamon.kr/rest-api/