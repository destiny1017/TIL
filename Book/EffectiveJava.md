이펙티브 자바, Joshua Bloch
===

## 1장, 객체 생성과 파괴
### 1. 생성자 대신 정적 팩터리 메서드를 고려햐라   
 - 정적 팩터리 메서드가 가지는 장점 5가지
   - 이름을 가질 수 있어 생성 행위의 필요조건과 결과를 좀 더 명시적으로 드러낼 수 있다.
   - 호출될 떄마다 인스턴스를 새로 생성하지 않아도 된다. 플라이 웨이트 패턴 등을 통해 빈번한 생성이 일어나는 객체를 캐싱하여 생성 비용을 줄일 수 있다.
   - 반환 타입의 하위 객체(자식클래스)를 반환할 수 있는 능력이 있다. 이는 인터페이스화를 통해 매우 뛰어난 유연성을 가져갈 수 있는 특징이 된다.
   - 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다. 위의 장점과 마찬가지로 이는 객체 생성의 유연성을 크게 증가시킨다.
   - 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다. JDBC와 같은 서비스 제공자 프레임워크를 만드는 근간이 되는 기술로서, 추후에 새로운 클래스가 추가돼도 변경 클라이언트는 없이 팩터리 메서드 사용이 가능하다.
 - 정적 팩터리 메서드의 단점
   - 상속을 하려면 public이나 protected 생성자가 필요해 상속이 불가능해진다. 다만 이는 상속보다 조합을 강제하여 오히려 장점이라 볼수도 있따.
   - 정적 팩터리 메서드를 프로그래머가 찾기가 어렵다. 이를 위해 공통 규약을 따라 팩터리 메서드를 설계하는 게 좋다.

   ```java
   class StaticFactoryMethod {
   
      // from : 하나의 매개변수, 해당 타입의 인스턴스 반환
      Date d = Date.from(instant);
      
      // of : 여러 매개변수, 적합한 인스턴스 반환
      Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
      
      // valueOf : from과 of의 더 자세한 버전
      BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
      
      // instance or getInstance : 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지 않음
      StackWalker luke = StackWalker.getInstance(options);
      
      // create or newInstance : instance 혹은 getInstance와 같지만 매번 새로운 인스턴스를 반환한다.
      Object newArray = Array.newInstance(classObject, arrayLen);
      
      // get[Type] : getInstance와 같으나, 다른 클래스에서 생성할 때 쓴다.
      FileStore fs = Files.getFileStore(path);
   
      // new[Type] : newInstance와 같으나, 다른 클래스에서 생성할 때 쓴다.
      BufferedReader br = Files.newBufferedReader(path);
      
      // [type] : getType과 newType의 간결한 버전
      List<Complaint> litany = Collections.list(legacyLitany);
   
   }
   ```
 