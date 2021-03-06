
싱글톤 패턴이란
=
애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴. 생성자가 여러차례 호출되더라도 실제로 생성되는 객체는 하나고 최초 생성 이후에 호출된 생성자는 최초에 생성한 객체를 반환한다. **즉, 싱글톤 패턴은 단 하나의 인스턴스를 생성해 사용하는 디자인 패턴이다. (인스턴트가 필요 할 때 똑같은 인스턴스를 만들어 내는 것이 아니라, 기존의 인스턴스를 사용하게 한다)**

장점
=
- 고정된 메모리 영역을 얻으면서 한번의 new 로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있다.
-  싱글톤으로 만들어진 클래스의 인스턴스는 전역 인스턴스이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다. 
- DBCP(DataBase Connection Pool)처럼 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용한다. (쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록 객체등)
- 두번째부터는 객체 로딩 시간이 많이 줄어들어 성능이 좋아진다.


단점
=
-	싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우 다른 클래스의 인스턴스들 간에 결합도가 높아져 "개방-폐쇄 원칙"을 위배하게 된다. (객체지향 설계 원칙에 어긋남)
-	수정이 어려워지고 테스트하기 어려워진다
-	멀티쓰레드 환경에서 동기화처리를 안하면 인스턴스가 두개가 생성되는 경우가 발생할 수 있다.

멀티쓰레드에서 안전한 싱글톤 클래스, 인스턴스 만드는 법
=
**Holder에 의한 초기화(Initialization on demand holder idiom) :**
클래스안에 클래스(Holder)를 두어 JVM의 Class loader 매커니즘과 Class가 로드되는 시점을 이용한 방법

~~~
public class Somthing{
	private Somthing() {
	}
	
	private static class LazyHolder{
		public static final Somthing INSTANCE = new Somthing();
	}
	
	public static Somthing gtInstance(){
		return LazyHolder.INSTANCE;
	}
}
~~~
개발자가 직접 동기화 문제에 대해 코드를 작성하고 문제를 회피하려 한다면 프로그램 구조가 그 만큼 복잡해지고 비용 문제가 생길 수 있고 특히 정확하지 못한 경우가 많다. 그런데 이 방법은 **JVM의 클래스 초기화 과정에서 보장되는 원자적 특성을 이용하여 싱글턴의 초기화 문제에 대한 책임을 JVM에 떠넘긴다.** Holder안에 선언된 instance가 static이기 때문에 클래스 로딩시점에 한번만 호출될 것이며 final을 사용해 다시 값이 할당되지 않도록 만든 방법이다.

---
출처: 
https://jeong-pro.tistory.com/86

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NTAxNjcyNDYsLTYzMzc3NjM3MF19
-->