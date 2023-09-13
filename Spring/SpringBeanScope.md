## 스프링의 빈스코프

- 스프링 빈 스코프란 스프링 컨테이너 안에서 빈이 생존하는 범위를 의미한다.
- 기본적으로 스프링 빈스코프의 범위는 아래와 같이 나뉜다.
  - 싱글톤 스코프
  - 프로토타입 스코프
  - 웹 스코프
    - Request 스코프
    - Session 스코프
    - Application 스코프
    - WebSocket 스코프
- scope를 따로 지정하지 않으면 설정되는 default 값은 싱글톤 스코프이다.
- 스프링 부트에서 빈스코프를 설정하는 가장 쉬운 방법은 @Scope 어노테이션을 이용하는 것이다.
  ```java
  @Component
  @Scope(value = "prototype")
  public class SampleBean {
      
  }
  ```
  
1. #### 싱글톤 스코프
   - 스프링 빈의 기본값이다. 일반적인 스프링 빈의 생명주기를 그대로 따르는 스코프로서 별다른 조작이 없는 한 애플리케이션 시작부터 종료까지 단 하나의 빈만 생성되고 클라이언트에 제공된다.
2. #### 프로토타입 스코프
   - 프로토타입 스코프는 클라이언트가 빈의 조회를 요청할 때마다 매번 새로운 빈을 생성해서 반환한다.
   - 스프링 컨테이너는 프로토타입 스코프의 빈에 대해서는 생성과 초기화까지만 관여하기 때문에 소멸에 대해서는 클라이언트에서 직접 관리해야한다. @Predestroy 또한 프로토타입 스코프에서는 동작하지 않는다.
   - #### 싱글톤 스코프 내에서 프로토타입 스코프를 사용할 때의 문제점
     - 만일 프로토타입 스코프 빈이 초기화된 클래스가 싱글톤 빈이라면, 클라이언트에서는 이 싱글톤 내의 프로토타입 빈의 조회를 아무리 요청해도 최초 초기화된 빈만을 반환하게 된다. 이런 상황에 싱글톤 빈 내에서 프로토타입 빈을 프로토타입 생명주기에 맞게 사용하려면 다음과 같이 사용해야 한다.
       1. 프로토타입 빈 메서드의 호출마다 ApplicationContext에서 새로운 빈을 요청하여 사용
       2. ObjectProvider로 래핑해서 빈을 사용
     - a 방식의 경우, 문제 자체는 해결이 되지만 문제는 클래스가 스프링에 강하게 결합되어 단위 테스트가 어려워진다는 단점이 있다.
     - b 방식이 위의 단점의 해결을 위해 나온 방식으로, ObjectProvider는 스프링이 아닌 자바 표준 라이브러리이므로 단위 테스트가 쉽고 다른 컨테이너에서도 사용할 수 있다.
     ```java
     public class SampleSingletoneBean {
        
        @Autowired
        private ObjectProvider<PrototypeBean> prototypeBeanProvider;
        
        public int logic() {
            PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
            prototypeBean.addCount();
            int count = prototypeBean.getCount();
            return count;
        }
     }
     ```
     
3. #### Request 스코프
   - 이 스코프는 클라이언트의 request 요청과 함께 빈이 생성되고, 트랜잭션을 처리후 response 시점에 빈이 파괴되는 스코프이다.
   - 이 스코프의 문제점은, 생성 시점이 request요청 시점이기 때문에 그냥 request스코프만 설정해둔 빈을 다른 클래스에 초기화하려고 하면 어플리케이션 구동시점에 에러가 발생한다. 구동시 스프링 컨테이너가 해당 빈을 초기화 하려고 시도하지만 아직 request가 들어오지 않았기 때문에 빈이 아직 생성되지 않아 빈을 찾을 수 없기 때문이다.
   - 이는 프로토타입 빈과 같이 ObjectProvider로도 생성 시점을 지연시켜 해결할 수 있지만, 이보다 더 간단한 방법은 @Scope 어노테이션의 프록시 기능을 이용하는 것이다.
     ```java
     @Component
     @Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
     public class RequestScopeBean {
     }
     ```
   - 프록시 모드를 이용하면, 생성 시점에는 해당 클래스를 상속받은 프록시를 생성하여 주입하였다가, 실제 사용 시점에는 프록시가 본래 객체를 호출하는 식으로 동작하기때문에 에러를 피할 수 있게 된다.
4. #### Session 스코프
   - 세션의 생명주기와 함께하는 스코프이다.
5. #### Application 스코프
   - 서블릿 컨텍스트(ex.TomcatServletContext)의 생명주기와 함께하는 스코프이다.
6. #### WebCoket 스코프
   - 웹 소캣의 생성명주기와 함께하는 스코프이다.