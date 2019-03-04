GraphQL 타입시스템
=
GraphQL 쿼리의 형태가 결과와 거의 일치하기 때문에 서버에 대해 모르는 상태에서 쿼리가 반환할 경과를 예측할 수 있습니다. 하지만 **서버에 요청할 수 있는 데이터에 대한 정확한 표현을 갖는 것이 좋습니다.** 어떤 필드를 선택 할 수 있는지, 어떤 종류의 객체를 반환할 수 있는지, 하위객체에서 사용할 수 있는 필드는 무엇인지, 이것이 바로 스키마가 필요한 이유 입니다.
모든 GraphQL 서비스는 해당 서비스에서 쿼리 가능한 데이터들을 완벽하게 설명하는 타입들을 정의하고, 쿼리가 들어오면 해당 스키마에 대해 유효성이 검사된 후 실행됩니다.

객체 타입과 필드
=
GraphQL 스키마의 가장 기본적인 구성 요소는 객체 타입입니다. 객체 타입은 서비스에서 가져올 수 있는 객체의 종류와 필드를 나타냅니다. GraphQL 스키마 언어에서는 다음과 같이 표현할 수 있습니다.
~~~
type Person{
	name:String!
	appearsIn: [Episode]!
	}
~~~
- **Person는 객체 타입 입니다.** 즉 필드가 있는 타입입니다. 스키마의 대부분은 객체 타입입니다.
- **name과 appearIn은 Person 타입의 필드입니다.** 즉 name 과 appearIn은 GraphQL 쿼리의 Person 타입에서 어디든 사용할 수 있는 필드입니다
- **String 은 내장된 스칼라 타입 중 하나입니다.** GraphQL 객체 타입은 이름과 필드를 가지지만, 어떤 시점에서 이 필드는 구체적인 데이터로 해석되어야 하기 때문에 스칼라 타입을 사용합니다. (**GraphQL에서의 스칼라 타입 : Int, Float, String, Boolean, ID**-ID 스칼라 타입은 String과 같은 방법으로 직렬화되지만, ID로 정의하는 것은 사람이 읽을 수 있도록 하는 의도가 아니라는 것을 의미합니다) 	
- **String! 은 필드가 non_nullable임을 의미합니다.** 즉, 이 필드를 쿼리할 때 GraphQL 서비스가 항상 값을 반환한다는 것을 의미합니다.
- **[Episode]! 는 Episode 객체의 배열을 나타냅니다.** 또한 non-nullable이기 때문에 appearsIn 필드를 쿼리할 때 항상 0개 이상의 아이템을 가진 배열을 기대할 수 있습니다.

인자
=
객체 타입의 모든 필드는 0개 이상의 인수를 가질 수 있습니다.
~~~
type Starship{
	length(unit : LengthUnit = METER) : Float
}
~~~
length 필드는 하나의 인자 unit을 가집니다. 인자는 필수거나 옵셔널일 수 있습니다. 인자가 옵셔널인 경우 기본값을 정의할 수 있습니다 **unit 인자가 전달되지 않으면 기본적으로 METER로 설정됩니다**

쿼리타입&뮤테이션타입
=
스키마 대부분의 타입은 일반 객체 타입이지만 스키
	
	


https://graphql-kr.github.io/learn/schema/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NzkxODQxNzYsLTkyNjkzNTU0M119
-->