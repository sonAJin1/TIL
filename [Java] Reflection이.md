Reflection이란
=

리플렉션이란 **구체적인 클래스 타입을 알지 못해도, 그 클래스의 메소드, 타입, 변수들을 접근할 수 있도록 해주는 자바 API입니다.** 

그렇다면 구체적인 클래스 타입을 알지 못하면 메소드를 실행하지 못하는지 살펴보겠습니다. 

~~~
public class Person {
	public void speak(){
		//doSomeThing
	}
}

public class Main{
	public static void main(String[] args){
		Object person = new Person();
		person.speak(); // 컴파일 에러
	}
}
~~~

위의 코드 블록에서 컴파일 에러가 나는 이유는 모든 클래스의 조상 클래스인 Object라는 타입으로 Person 클래스의 인스턴스는 담을 수 있지만 사용가능한 메소드는 Object의 메소드와 변수들 뿐이기 때문에, person의 메소드는 사용할 수 없습니다.

이런식으로 구체적인 타입의 클래스를 모를 때 사용하는게, 리플렉션입니다. 코드를 작성할 시점에는 어떤 타입의 클래스를 사용하지 모르는 경우가 있습니다. 이럴 때는 실행할 시점, 런타임에 지금 실행되고 있는 클래스를 가져와서 실행해야합니다.
 

Reflection의 사용
=
Reflection은 위에 언급했던 것 처럼 실행중인 자바프로그램 내부를 검사하고 내부의 속성을 수정할 수 있도록 합니다.  자바 클래스 파일은 바이트 코드로 컴파일 되어 Static 영역에 위치하기 때문에 클래스 이름만 알고 있다면, 언제든 이 영역을 뒤져서 클래스에 대한 정보를 가져올 수 있습니다. 아래는 가져올 수 있는 정보들입니다.

- Class Name
- Class Modifiers (public, private, synchronized 등)
- Package Info
- Superclass
- Implemented Interfaces
- Constructors
- MethodsFields
- Annotations

----
참조:
https://gyrfalcon.tistory.com/entry/Java-Reflection
https://brunch.co.kr/@kd4/8
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgwODQ4ODU2NF19
-->