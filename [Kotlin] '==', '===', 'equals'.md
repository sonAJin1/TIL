Structural Equality ('==')
=
Kotlin에서 `== 연산자`는 두 변수의 **데이터를 비교**하는 데 사용됩니다. 반면 Java 또는 다른 언어에서는 일반적으로 참조를 비교하는데 사용됩니다. '같은 데이터가 아님' 을 나타내는 연산자는 `!=` 로 나타냅니다.

Referential Equality ('===')
=
Kotlin에서 `=== 연산자`는 두 변수 또는 객체의 참조를 비교하는 데 사용됩니다. `true`는 두 객체 또는 변수가 동일한 객체를 가리키는 경우에만 해당됩니다. '같은 객체가 아님'을 나타내는 연산자는 `!==`로 나타냅니다.


'.equals' 메서드
=
Kotlin에서 `.equals(other:Any?)` 메서드는 `==` 연산자와 마찬가지로 변수 또는 객체의 내용을 비교하지만 `==`연산자와는 `Float` 또는  `Double` 를 비교할 때 차이가 있습니다. 

`equals`는 부동 소수점 연산을 위해서 IEEE 754 표준을 따르고 있습니다.

> **부동 소수점이란 :**  '부동(浮動)'은 '고정'에 반대되는 표현으로 '위치가 변경된다'는 의미이다. 즉, 소수점의 위치를 변경할 수 있다. 제한된 크기의 메모리 공간에서 표현할 수 있는 수의 범위를 키우기 위해 사용하며 대신 정확도가 희생될 수 있다. (그래서 블록체인에서는 floating point 연산을 지원하지 않습니다.) 
>
>참고 :http://egloos.zum.com/studyfoss/v/4956717

> **NaN:** "Not a number (숫자가 아님)"의 약어. 실수나 복소수가 아닌 값을 나타낸다. 0/0, inf/inf(무한대)와 같은 표현식은 NaN을 반환한다.

-	`NaN`은 자기 자신 과 같은 것으로 간주한다
-	`NaN`은 POSITIVE_INFINITY를 포함하여 다른 요소보다 더 크게 고려한다
-	-0.0은 0.0보다 작은수


Data Class 와 Class 값 비교
=
아까 위에서 `==`와 `equals`가 객체의 내용을 비교한다고 했습니다.
하지만 이것은 `Data Class`일 때의 경우이고 `Class`의 변수값을 비교할 때는 조금 다르게 작동합니다. 아래의 예시를 보겠습니다.

~~~

data class Person (val name: String){

	val person1 = Person("Tom")
	val person2 = Person("Sam")

	println(person1 == person2) 	 // true
	println(person1.equals(person2)) // true
	
	println(person1.name == person2.name)       //true  
	println(person1.name.equals(person2.name))  //true
}

--------------------------------------------------

class Person (val name: String){

	val person1 = Person("Tom")
	val person2 = Person("Sam")

	println(person1 == person2) 	 // false
	println(person1.equals(person2)) // false
	
	println(person1.name == person2.name)       //true  
	println(person1.name.equals(person2.name))  //true
}


~~~
일반 클래스 인 경우 컴파일러는 내용이 같더라도 두 객체를 다른 객체로 간주하지만 객체가 data 클래스인 경우 컴파일러는 내용이 동일하면 데이터를 비교하고 `true/false`값을 출력합니다.



-----
참고:
https://medium.com/@agrawalsuneet/equality-in-kotlin-and-equals-d8373ef529f1
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTkzOTQ4MDg1XX0=
-->