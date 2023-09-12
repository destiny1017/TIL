## 함수형 프로그래밍(Functional Programming) 

- #### 프로그래밍 패러다임의 변화
  - 명령형 프로그래밍 : 무엇을 할지보다 어떻게 할 것인지를 기술하는 방식
    - 절차지향 프로그래밍 : 진행되어야할 순차적인 처리과정을 표현하는 방식
    - 객체지향 프로그랴밍 : 객체들의 집합과 협력관계를 통해 프로그램의 상호작용을 표현하는 방식
  - 선언형 프로그래밍 : 어떻게 할지보다 무엇을 할 것인지를 기술하는 방식
    - 함수형 프로그래밍 : 순수 함수를 조합하여 프로그램을 만드는 방식
    
- #### 함수형 프로그래밍의 등장
  - 기존의 명령형 프로그래밍으로 개발을 해오던 개발자들은 소프트웨어의 규모가 커지고 유지보수 기간이 길어질수록 방대해지는 스파게티 코드를 유지보수하기가 매우 어렵다는 것을 깨달았다. 그리고 이를 해결하기위한 방안으로 함수형 프로그래밍이라는 기법에 관심을 갖게 되었다. 이는 프로그램 작동 방식에 대한 거의 모든 것을 작은 순수 함수로 나누어 문제를 해결하는 방식으로, 가독성을 높이고 유지보수를 용이하게 해준다.

- #### 함수형 프로그래밍의 특징
  > 부수 효과가 없는 순수 함수를 1급 객체로 간주하여 파라미터나 반환값으로 사용할 수 있으며, 참조 투명성을 지킬 수 있다.
  - 부수효과(Side Effect)란?
    - 변수의 값이 변경됨
    - 자료구조를 제자리에서 수정함
    - 객체의 필드값을 설정함
    - 예외나 오류가 발생하여 실행이 중단됨
    - 콘솔 또는 파일 I/O가 발생함
  - 순수함수(Pure Function)란?
    - 함수 자체가 독립적이며 부수효과가 없고 Thread-safe하다.
    - Thread-safe 특성으로인해 병렬처리를 동기화 없이 진행가능하다.
  - 1급 객체(First-Class Object)
    - 변수나 데이터 구조 안에 담을 수 있다.
    - 파라미터로 전달할 수 있다.
    - 반환값으로 사용할 수 있다.
  - 참조 투명성(Referential Transparency)
    - 동일한 인자에 대해 항상 동일한 결과를 반환해야 한다.
    - 참조 투명성을 통해 기존의 값은 변경되지 않고 유지된다(Immutable Data)   
     
  명령형 프로그래밍의 함수와 함수형 프로그래밍의 함수의 가장 큰 차이는 부수효과의 유무이다. 프로그램 동작의 흐름을 순수 함수로 표현하고, 부수효과를 없애 직관적으로 이해할 수 있도록 하는 데에 함수형 프로그램의 목적이 있다. 그리고 이런 순수함수의 특징으로 인해 병렬환경에서 동시성 제어에 대한 비용을 줄여주는 효과도 있다.

- #### 예시

  ```java
    public class WordProcessTest {
    
        private final List<String> words = Arrays.asList("TONY", "a", "hULK", "B", "america", "X", "nebula", "Korea");
    
        @Test
        void wordProcessTest() {
            String result = words.stream()
                    .filter(w -> w.length() > 1)
                    .map(String::toUpperCase)
                    .map(w -> w.substring(0, 1))
                    .collect(Collectors.joining(" "));
    
            assertThat(result).isEqualTo("T H A N K");
        }
    }
  ```
    이와 같은 Stream, Lambda 방식의 코드가 함수형 프로그래밍의 대표적인 예이다. 코드를 하나하나 살펴보면 위에서 설명한 함수형 프로그래밍의 특징이 모두 드러난다. 어떻게하는지보다 함수명으로 무엇을 하는지를 기술하고 있고, 어떤 함수도 기존의 값을 변화시키지 않는다.


###### Reference : https://mangkyu.tistory.com/111