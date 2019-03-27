중첩 클래스는 왜 사용하는가?
=
-	클래스들의 논리적인 그룹을 나타낼 때 쓴다. 주로 model 객체에서 상위모델과 하위모델이 있을 때 사용 (Static Nested Class를 많이 사용한다)
-	향상된 캡슐화
-	좋은 가독성과 유지보수성

중첩 클래스의 종류
=
![중첩 클래스의 종류](https://img1.daumcdn.net/thumb/R1920x0/?fname=http://cfile5.uf.tistory.com/image/99DA873B5AC20B79183F1C)

1. **내부 클래스:** 밖에 있는 클래스는 내부 클래스를 멤버 변수처럼 사용할 수 있다. 사용하려면 new로 인스턴스를 만들어야한다. 내부클래스는 자신의 밖에 있는 클래스의 자원을 직접 사용할 수 있다.

~~~

class Outer{
	public class Inner {
	}
}

** 객체 생성 **
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();

~~~


2. **정적 중첩클래스:** 위의 내부클래스와 비슷하나, static 으로 선언한다. 정확히는 Static Nested Class 라고 한다. 밖에 있는 변수와 메소드 중에 static이 붙은 것들은 사용할 수 있다. **Inner 클래스를 static 으로 생성하면 클래스 자체가 메모리 상에 객체로 생성된 것이 아니다.** 단지 Outer에게 있어 static 형태로 존재하는 멤버 변수처럼 여겨진다. **즉, static 이 붙은 Inner 클래스는 단지 static이 붙은 전역변수 정도의 의미이다. 객체 자체가 생성되지는 않았으므로 new로 생성해줘야한다.**

-	**내부 클래스와의 차이 :** 내부 클래스는 밖에 있는 클래스의 자원을 마음대로 사용할 수 있지만, 중첩클래스는 static 키워드가 안붙었다면 사용할 수 없다. **Outer 클래스의 객체가 없어도 Inner 클래스의 객체 생성이 가능하다.**

~~~

class Outer {
	public static class Inner{
	}
}

** 객체 생성 **
Outer.Inner inner = new Outer.Inner();

~~~


3. **지역 클래스:** 메소드 내부에 글래스를 정의하는 경우이다. 마치 메소드 내의 지역변수처럼 쓰인다. 메소드 내부에서 new 한뒤 사용해야한다. 메소드 밖에서 사용할 수 없다.

~~~

class Outer{
	
	public void function(){
		String local;
		
		class Inner{
		
		}
	}
}
~~~

4. **익명 클래스:** 익명 클래스는 인스턴스 이름이 없다. new와 동시에 부모클래스를 상속받아 내부에서 오버라이딩해서 사용한다. **상속은 받아야하지만, 한번만 사용할 것이라서 extends 문법을 굳이 사용하지 않을 때 주로 사용한다.** 익명클래스 외부의 자원은 final 키워드가 붙은 것만 사용할 수 있다. 아래의 모양처럼 Inner 클래스가 이미 선언되어있어야 한다. **Inner 클래스를 바로 상속받고 Overriding해서 쓰는 구조이다.

~~~

class Inner {
	
}

class Outer {
	public void function(){
		new Inner(){
			overriding ...
		}
	}
}
~~~


------
참고 : https://sjh836.tistory.com/145
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwMjEyODY5OF19
-->