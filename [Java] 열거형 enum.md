열거타입 enum
=

열거 타입은 일정 개수의 상수 값을 정의한 다음, 그 외의 값은 허용하지 않는 타입이다. 자바에서 열거 타입을 지원하기 전에는 다음 코드처럼 정수 상수를 한 묶음 선언해서 사용하곤 했다.

~~~

public static final int APPLE_HI	= 0;
public static final int APPLE_FUJI	= 1;
public static final int APPLE_GRANNY_SMITH	= 2;

public static final int ORANGE_HI	= 0;
public static final int ORANGE_TEMPLE	= 1;
public static final int ORANGE_BLOOD	= 2;

~~~
정수 열거 패턴 기법은 타입 안전을 보장할 방법이 없으며 표현력도 좋지 않다. 오렌지를 건내야 할 메서드에 사과를 보내고 동등 연산자로 비교하더라도 컴파일러는 아무런 경고 메세지를 출력하지 않는다.

~~~

public enum Apple{ HI,FUJI,GRANNY_SMITH }
public enum Orange{ HI,TEMPLE,BLOOD }

~~~

자바 열거 타입을 뒷밭침 하는 아이디어는 단순하다. 열거 타입 자체는 클래스이며, 상수 하나당 자신의 인스턴스를 하나씩 만들어 public static final 로 공개한다. 열거 타입은 밖에서 접근할 수 있는 생성자를 제공하지 않으므로 사실상 final이다. 따라서 **클라이언트가 인스턴스를 직접 생성하거나 확장 할 수 없으니 열거 타입 선언으로 만들어진 인스턴스들은 딱 하나씩만 존재함이 보장된다.** 

열거 타입에는 임의의 메서드나 필드를 추가할 수 있고 임의의 인터페이스를 구현하게 할 수도 있다. 코틀린 문법으로 살펴보자.

**초기화:** 
~~~
enum class Color(val rgb: Int) {
        RED(0xFF0000),
        GREEN(0x00FF00),
        BLUE(0x0000FF)
}
~~~

**익명 클래스:** 
~~~
enum class ProtocolState {
    WAITING {
        override fun signal() = TALKING
    },

    TALKING {
        override fun signal() = WAITING
    };

    abstract fun signal(): ProtocolState
}
~~~

**열거 형 클래스에서 인터페이스 구현:**
~~~
enum class IntArithmetics : BinaryOperator<Int>, IntBinaryOperator {
    PLUS {
        override fun apply(t: Int, u: Int): Int = t + u
    },
    TIMES {
        override fun apply(t: Int, u: Int): Int = t * u
    };

    override fun applyAsInt(t: Int, u: Int) = apply(t, u)
}
~~~

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzMDQ3NTIwNl19
-->