## OOP(Object Oriented Programming)

- #### 객체지향 프로그래밍
    - 객체지향 프로그래밍이란, 절차적으로 작성된 코드의 흐름과 함수의 호출이라는 프로그래밍 패러다임에서 벗어나, 상태와 행위를 가진 다양한 객체를 정의하고 생성하며, 해당 객체들 간의 유기적인 상호작용을 통해 프로그램을 완성시켜나가는 프로그래밍 방법론을 일컫는다.
    - 객체지향의 장단점

      **장점**

        - 코드의 재사용이 용이 - 남이 만든 클래스를 가져와 사용가능, 상속을 통한 확장 가능
        - 유지보수의 용이 - 객체별로 역할과 책임이 잘 분담되어 있으므로 해당 객체만 적당히 수정하면 된다
        - 대형 프로젝트에 적합 - 도메인 별로 모듈화 시켜 개발하면 역할 분담이 용이하다

      **단점**

        - 설계가 복잡하고 오랜 시간이 소요됨
        - 객체가 많을수록 용량이 커짐
        - 처리속도가 상대적으로 느림

- #### SOLID 원칙
    - **SRP**(단일책임의 원칙: Single Responsibility Principle)
        - 클래스가 제공하는 모든 서비스는 하나의 책임을 수행하는 데에 집중되어 있어야 함.
        - 클래스를 변경해야하는 이유는 오직 하나 뿐이어야 함.
    - **OCP**(개방폐쇄의 원칙: Open Close Principle)
        - 소프트웨어의 구성요소(컴포넌트, 모듈, 클래스, 함수)는 확장에는 열려있고 변경에는 닫혀있어야 함.
        - 변경될 것과 변경되지 않을 것을 엄격히 구분하여 인터페이스를 정의하고, 구현보다 이 인터페이스에 의존적이게 설계.
    - **LSP**(리스코브 치환의 원칙: The Liskov Subsitution Principle)
        - 서브타입은 언제나 기반타입으로 교체할 수 있어야 한다.
        - 기반타입은 서브타입의 규약을 지켜야하고, 서브타입으로 생성 하여 기반타입으로 초기화하더라도 이상 없이 동작해야한다.
    - **ISP**(인터페이스 분리의 원칙: Interface Segregation Principle)
        - 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야함.
        - 즉, 하나의 일반적인 인터페이스보다는, 여러개의 구체적인 인터페이스가 낫다.
    - **DIP**(의존성 역전의 원칙: Dependency Inversion Principle)
        - 의존관계를 설정할 때는 고수준 모듈에 의존적이게 설계해야한다.
        - 즉, 변하기 쉬운 저수준 모듈에 의존적이게 설계하지 말라는 뜻. 클래스 보다는 인터페이스 상속을 추구.
- #### SOLID 클래스 변화 예시
    - Guitar Class
    1. **S - 단일책임원칙 적용**

       Guitar (고정정보인 시리얼 넘버만을 가짐)

       GuitarSpec (유동정보인 스펙정보를 가짐)

    2. **O - 개방폐쇄의 원칙 적용**
        - 추상화 시켜 인터페이스를 생성, 상속하고 최대한 변경하지 않기

       StringInstrument

       Guitar

       Violin

       …

       StringInstrumentSpec

       GuitarSpec

       ViloinSpec

       …

    3. **L - 리스코브 치환의 원칙**
        
       *서브타입은 언제나 기반타입으로 변경가능해야함*

        1. 생성자 클래스가 상속중인 부모타입으로 초기화

            ```Groovy
            Collection<String> collection = new ArrayList<>();
            ```

        2. 생성자를 같은 부모를 가진 다른 클래스로 교체

            ```Groovy
            Collection<String> collection = new HashSet<>();
            ```

        - 위와 같은 상황에서 collection.get();과 같은 공통 메서드를 사용해도 이상이 없어야함
        
    4. **I - 인터페이스 분리의 원칙**
        
        ```Groovy
        public interface Car{
        	run();
        	break();
        	openTrunk(); // 공통함수 아님, 트렁크 없는 차 있을 수 있음. 인터페이스 분리필요
        }
        ```

    5. **D - 의존성 역전의 원칙**
        
        객체는 저수준 모듈보다 고수준 모듈에 의존적이어야함
        
        ```Groovy
        public interface Character {
        	Sword weapon; // 무기라는 고수준 모듈 아래의 검이라는 저수준 모듈에 의존중
        }
        ```
        
        ```Groovy
        public interface Character {
        	Weapon weapon; // 고수준 모듈을 의존하도록 변경
        }
        ```

- **객체지향의 4가지 주요 특징**
    - **캡슐화**(Encapsulation)
        - 데이터와 처리 함수를 하나로 묶는 것.
        - 캡슐화는 정보은닉 특성을 포함한다.
        - 정보은닉은 외부 객체에 자신의 정보를 숨기고 자신의 함수를 통해서만 접근 가능하게 하는 특성
    - **상속**(Inheritance)
        - 이미 정의된 상위 클래스의 속성과 함수를 하위 클래스가 물려받는 것.
        - 물려받은 모든 속성과 연산은 하위클래스에서 재정의하지 않고도 즉시 사용할 수 있다.
    - **추상화**(Abstraction)
        - 여러 객체들의 고유한 특징을 제외하고 공통적인 특징들을 찾아내어 모델링하는 것
    - **다형성**(Polymorphism)
        - 프로그램 언어의 각 요소들(변수, 함수, 객체)이 다양한 자료형에 속하는 것이 허가되는 성질
        - 오버로딩, 오버라이딩 등이 대표적인 다형성의 예이다.
- #### 추상클래스, 인터페이스
    - 추상클래스는 클래스에 abstract를 선언했거나, abstract인 메서드가 하나라도 존재하는 클래스
    - 자식클래스가 추상클래스의 기능을 이용하고 확장하기 위해 사용하는 클래스
    - 상속으로 추상클래스와의 연관관계를 형성한다. 다중상속 불가능
    - 추상클래스는 자식클래스와의 관계가 Is-a 이지만, 일부 동작에 있어 차이점이 필요할 때 사용한다.
    - 인터페이스는 전체 메소드가 구현부 없이 선언부만 있는 추상메서드로 이루어져있다.
    - 추상클래스와 달리 기능의 이용,확장의 목적이 아닌 기능 구현의 강제를 위해 사용한다.
    - implements 로 구현하며, 다중 상속이 가능하다.
    - 같은 인터페이스를 상속받은 클래스들간의 기능 구조의 동일성을 보장한다.