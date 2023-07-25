
## SpringBoot의 ExceptionHandler

- Spring은 기본적으로 내부에서 에러가 발생할 경우 에러를 처리할 BasicErrorController를 구현해뒀다.
- 에러가 발생하면 /error uri로 error controller를 찾아가며, 기본 에러 페이지인 whitelabel error페이지를 띄운다.
- Java에서는 에러처리를 위해 기본적으로 try/catch문을 활용해야 하지만, 이는 코드의 중복을 일으키고 가독성을 떨어뜨리는 주범이다.
- 이를 해결하기위해 SpringBoot에서는 ExceptionHandler라는 어노테이션을 제공한다.
- 기본적인 사용법은 CustromErrorHandler 클래스를 생성하고, @ControllerAdvice 또는 @RestControllerAdvice를 선언한다.
- 그러면 이후로는 프레임워크 내에서 발생하는 에러는 이 클래스를 먼저 찾아오게 된다.
- 그리고 Hadler에 도착한 각각의 에러를 처리하기위해서는 @ExceptionHandler어노테이션을 설정해줘야한다.
- @ExceptionHandler({Exception클래스명.class}) 와 같은 방식으로 어떤 Exception을 처리할지 지정하여 처리 메서드를 작성한다.
- 메소드에 @ResponseStatus 어노테이션을 붙이면 http 상태 코드를 변경할수도 있다.
- RuntimeException 클래스를 상속하면 기본적인 Exception 핸들러들을 모두 상속받아 기본 Exception들은 모두 여기서 받도록 설정할 수 있다.

* 스프링부트의 예외처리 흐름은 아래와 같다
  ![image](https://github.com/destiny1017/TIL/assets/44860334/824d8498-76ce-4be9-bc18-540918ded68f)

