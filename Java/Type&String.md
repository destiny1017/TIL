### Type

- **접근제어자**
    - 객체지향 설계원칙 중 캡슐화(Encapsulation)를 구현하는 기법.
    - 접근 시도 지점을 기준으로 클래스 내 데이터들에 대한 접근 허용 범위를 결정한다.
    - 외부에서의 접근 및 수정을 막음으로서 객체간의 결합도를 낮추는 효과가 있다.
    - 접근제어자 종류
        1. private : 모든 외부의 접근을 막고 오직 자기 자신에서만 접근 가능
        2. default : 동일 패키지 내에서의 접근만을 허용. ex) jar배포 후 라이브러리로 호출하여 사용시 접근 불가
        3. protected : 동일 패키지 내에서의 접근과, 외부의 경우 해당 패키지를 상속 받았을 경우에만 접근을 허용
        4. public : 모든 외부의 접근을 허용
- **Wrapper Class**
    - 기본형 데이터타입(primitive type)을 Object와 같이 사용하기 위한 클래스
    - primitive type은 null값을 대입할 수 없어서 주로 null을 허용해야할 경우 Wrapper Class를 사용한다.
    - 래퍼클래스로 박싱이 이루어지면 오브젝트이기 때문에 == 연산자로 값 비교가 불가능
        - String의 경우 리터럴로 생성할 경우 String pool에서 같은 값을 가진 데이터를 찾아 주소를 반환하기 때문에 == 비교 가능
    - 기본형 ↔ 객체형 간의 타입 전환은 값 초기화 시 자동으로 boxing / unboxing이 발생된다.
- **Generic**
    - 클래스 내부에서 사용할 타입을 외부에서 지정해주는 기법
    - 모든 객체타입을 허용한다는 점에서 Object와 비슷하지만, Object를 사용할 경우에는 잦은 형변환과, ClassCastException의 위험성이 있고 가독성의 문제등등이 있다.
    - 그리고 코드 작성 시 어떤 타입을 사용할 것인지 명확하게 지정해줘야 하므로 잘못 지정할 시 컴파일 타임에 에러를 발견할 수 있다.

### String

- **String vs Stringbuffer / Stringbuilder**
    - String은 불변의 속성이 있어서 문자열이 변경될 때마다 새로운 메모리에 객체를 생성하고 기존 문자열은 GC에 남는다.
    - String 리터럴은 Runtime Constant Pool내의 String Constant Pool을 참조한다.
    - 그러므로 문자열의 추가/수정/삭제가 빈번하게 발생하는 경우라면 String보다 Stringbuilder/Strinfbuffer를 사용하는 게 낫다.
- Stringbuilder/buffer는 가변성이 있어 빈번한 변경에 유리한 점은 동일하지만, buffer는 builder와 다르게 동기화를 지원한다.
- 대신 단일 스레드에서는 builder가 buffer보다 효율적이므로, 멀티스레드 환경에서 동기화가 필요할 때 buffer를 사용하면 된다.