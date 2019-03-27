
내부 클래스 GC
=
내부 클래스는 외부 클래스의 멤버에 접근할 수 있다. 즉, 내부 클래스는 암시적으로 외부 클래스에 대한 참조를 가진다. 따라서 내부 클래스로 정의된 스레드는 스레드가 실행되는 동안 외부 클래스에 대한 참조를 유지하기 때문에 **외부 클래스의 모든 객체는 스레드가 실행되는 한 내부 클래스와 함께 메모리에 있어야 한다.**

정적 내부 클래스 GC
=
정적 내부 클래스는 외부 클래스의 정적멤버에만 접근할 수 있다. 외부 클래스 인스턴스 멤버이기 때문이다. 따라서 내부 클래스로 정의된 스레드는 외부 객체 자체가 아닌 외부 객체 클래스에 대한 참조만 유지한다. **즉, 외부 객체는 자신을 참조하는 다른 객체가 사라지면 가비지 컬렉션 될 수 있다.**

단, 스레드를 생성할 때 Runnable 객체를 외부 클래스의 내부 클래스로 생성하면 Runnable 객체가 외부 클래스에 대한 참조를 유지하게 된다.이 때에는 해당 스레드가 끝날 때 까지 외부 클래스 객체는 가비지 컬렉션 되지 않는다.
~~~

** GC되지 않는 경우 **

public class Outer {
	public void method(){
		Samplethread sampleThread = new SampleThread();
		sampleThread.start();
	}
	private static class SampleThread extends Thread{
		public void run(){
		}
	}
}


** GC되는 경우(Runnable 객체를 외부 클래스의 내부 클래스로 생성) **

public class Outer{
	public void method(){
		SampleThread sampleThread = new SampleThread(new Runnable(){
			@Override
			public void run(){
			}
		}
	})
}

private static class SampleThread extends Thread{
	public SampleThread(Runnable runnable){
		super(runnable);
	}
}

~~~

이런 상황에서 발생할 수 있는 메모리 누수를 방지할 수 있는 방법은 무엇일까? 가장 중요한 것은 **작업을 다한 스레드는 꼭 종료시켜야 한다.** 핸들러를 사용할때는 메시지 큐에 보내진 메시지를 사용하지않으면 removeCallbacksAndMessages 메서드로 메시지를 종료시켜야한다.(handler.hasMessage 메소드 등을 사용하여 해당 메세지가 메시지 큐에 현재 존재하는지 확인 후 진행한다.)

만약 화면이 변경되야할 때 스레드가 유지되어야한다면, 액티비티가 새로 생기게 되는데 기존 스레드는 기존의 액티비티를 계속 참조해 액티비티가 GC 되지 않는 문제가 발생할 수 있다. (안드로이드에서 메모리 누수의 많은 원인 중 하나는 스레드와 안드로이드 구성 요소간 생명주기의 불일치로 발생한다) 따라서 **새로 생성되는 안드로이드 구성요소를 참조하도록 변경해야한다.**
구현 방법은 액티비티와 프래그먼트로 나뉜다.

-	**Activity :** 액티비티에서 스레드 유지는 onRetainNonConfigurationInstatnce()와 getLastNonConfigurationInstance() 메서드를 이용해 구현한다. 전자 메서드는 구성 변경 전에 콜백되고 새로운 액티비티 객체에 전달하고자 하는 객체를 반환해야한다. 스레드 유지를 위해서는 스레드를 반환하면 된다. 구성 변경 후에 새로운 액티비티의 onCreate나 onStart 메서드에서 후자 메서드를 호출해 반환값을 전달 받은 객체로 캐스팅하면 된다. 단, 구성 변경이 아닌 액티비티 재시작에서는 null이 반환된다.

-	**Fragment:** 프래그먼트에서는 Fragment.onCreate()에서 setRetainInstance(true)를 호출하면 된다. 그러면 프래그먼트는 설정 변경동안 유지되고 프래그먼트에서 실행한 스레드는 계속 살아있게 된다.



----
참조 : https://programmingfbf7290.tistory.com/entry/%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%A0%95%EC%A0%81-%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%97%90%EC%84%9C-GC%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%EC%85%98
https://programmingfbf7290.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%97%90%EC%84%9C-%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-%EB%B0%A9%EC%A7%80
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0NTUzMjYyOSwxNjQyOTgyMjU5XX0=
-->