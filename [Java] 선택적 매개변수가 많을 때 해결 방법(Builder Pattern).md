선택적 매개변수가 많을 때 해결 방법
=

정적 팩토리와 생성자에는 똑같은 제약이 있습니다. 선택적 매개변수가 많을 때 적절히 대응하기 어렵다는 점입니다. 이런 문제를  해결하기 위해서 3가지의 해결 방법을 들 수 있습니다.

**1. 점층적 생성자 패턴:** 
이런 문제를 해결하기 위한 첫번째 방법은 점층적 생성자 패턴(relescoping constructor pattern) 입니다. 이 방법은 필수 매개변수만 받는 생성자부터 선택 매개변수를 전부 다 받는 생성자까지 늘려가는 방식입니다. 

~~~
pulic class NutritionFacts{
	private final int servingSize;
	private final int servings;
	private final int calories;
	prifate final int fat;
}

public NutritionFacts(int servingSize, int servings){
	this(servingSize, servings, 0);
}

public NutritionFacts(int servingSize, inst servings, int calories){
	this(servingSize, servings, calories,0);
}

....

**호출**
NutritionFacts cocaCola = new NutritionFacts(240,8,100,35);

~~~

보통 이런 생성자는 사용자가 설정하길 원치 않는 매개변수까지 포함하기 쉬운데, 어쩔 수 없이 그런 매개변수에도 값을 지정해줘야 합니다. 이 예제에서는 매개변수가 4개 뿐이라 복잡해 보이지 않을 수 있지만, **매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵습니다.**

**2. 자바빈즈 패턴:** 
두번째 방법은 자바빈즈 패턴(JavaBeans Pattern)입니다. 매개변수가 없는 생성자로 객체를 만든 후, 세터(setter) 메서드들을 호출해 원하는 매개변수의 값을 설정하는 방식입니다.

~~~
pulic class NutritionFacts{
	private final int servingSize = 0;
	private final int servings = 0;
	private final int calories = 0;
	prifate final int fat = 0;
}

public NutritionFacts(){}

public void setServingSize(int val) {servingSize = val;}
public void setServings(int val) {servings = val;}
public void setCalories(int val) {calories = val;}
public void setFat(int val) {fat = val;}


**호출**
NutritionFacts cocaCola = new NutritionFacts();
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setFat(20);

~~~

코드가 더 길어지긴 했지만 인스턴스를 만들기 쉽고, 그 결과 더 읽기 쉬운 코드가 되었습니다. 하지만 **자바빈즈 패턴에서는 객체 하나를 만들려면 메서드를 여러 개 호출해야 하고, 객체가 완전히 생성되기 전까지는 일관성이 무너진 상태에 놓이게 됩니다.** 점층적 생성자 패턴에서는 매개변수들이 유효한지를 생성자에서만 확인하면 일관성을 유지할 수 있었는데, 그 장치가 사라진 것입니다. 이처럼 일관성이 무너지는 문제 때문에 **자바빈즈 패턴에서는 클래스를 불변으로 만들 수 없으며** 스레드 안전성을 얻으려면 프로그래머가 추가 작업을 해줘야 합니다.


**3. 빌더 패턴:**
세번째 방법은 점층적 생성자 패턴의 안전성과 자바빈즈 패턴의 가독성을 겸비한 빌더 패턴(Builder Pattern) 입니다. 클라이언트는 필요한 객체를 직접 만드는 대신,  필수 매개변수만으로 생성자를 호출해 빌더 객체를 얻습니다. 그런 후 빌더 객체가 제공하는 일종의 세터 메서드 들로 원하는 선택 매개변수들을 설정합니다. 빌더는 생성할 클래스 안에 정적 멤버 클래스로 만들어두는게 보통입니다.

~~~
public class NutritionFacts {
	private final int servingSize;
	private final int servings;
	private final int calories;
	private final int fat;

	public static class Builder{
		//필수 매개변수
		private final int servingSize;
		private final int serings;
		
		//선택 매개변수 - 기본값으로 초기화 한다.
		private int calories = 0;
		private int fat = 0;

		public Builder(int servingSize, int servings){
			this.servingSize = servingSize;
			this.servings = servings;
		}

		public Builder calories(int val){
			calories = val;
			return this;
		}
		public Builder fat(int val){
			fat = val;
			return this;
		}
		public NutritionFacts build(){
			return new NutritionFacts(this);
		}
	
		private NutritionFact(Builder builder){
			servingSize = builder.servingSize;
			servings = builder.servings;
			calories = builder.calories;
			fat = builder.fat;
		}
	}
}

**호출**
NutritionFacts cocaCola = new NutritionFacts.Builder(240,8).calories(100).fat(8).build();

~~~

이 클라이언트 코드는 쓰기 쉽고, 읽기 쉽습니다. **빌더 패턴은 파이썬과 스칼라에 있는 명명된 선택적 매개변수를 흉내 낸 것 입니다.** 여기에 잘못된 매개변수를 최대한 일찍 발견하려면 빌더의 생성자와 메서드에서 입력 매개변수를 검사하고, build 메서드가 호출하는 생성자에서 여러 매개변수에 걸친 불변식을 검사하자. 공격에 대비해 이런 불변식을 보장하려면 빌더로부터 매개변수를 복사한 후 해당 객체 필드들도 검사해야합니다.

**결론:**
생성자로는 누릴 수 없는 사소한 이점으로, 빌더를 이용하면 가변인수 매개변수를 여러 개 사용할 수 있습니다. 각각을 적절한 메서드로 나눠 선언하면 됩니다. 아니면 메서드를 여러번 호출하고 각 호출 때 넘겨진 매개변수들을 하나의 필드로 모을 수도 있습니다. 
하지만 객체를 만들려면 먼저 빌더부터 만들어야하고, 빌더 생성 비용이 크지는 않지만 성능에 민감한 상황에서는 문제가 될 수도 있습니다. **즉, 생성자나 정적 팩터리가 처리해야 할 매개변수가 많다면 빌더 패턴을 선택하는 것이 낫습니다.**

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5OTMyOTA2OV19
-->