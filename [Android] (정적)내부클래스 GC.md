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




----
참조 : https://programmingfbf7290.tistory.com/entry/%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%A0%95%EC%A0%81-%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%97%90%EC%84%9C-GC%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%EC%85%98
https://programmingfbf7290.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%97%90%EC%84%9C-%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-%EB%B0%A9%EC%A7%80
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0Mjk4MjI1OV19
-->