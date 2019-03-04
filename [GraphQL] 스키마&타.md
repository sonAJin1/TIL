GraphQL 타입시스템
=
GraphQL 쿼리의 형태가 결과와 거의 일치하기 때문에 서버에 대해 모르는 상태에서 쿼리가 반환할 경과를 예측할 수 있습니다. 하지만 **서버에 요청할 수 있는 데이터에 대한 정확한 표현을 갖는 것이 좋습니다.** 어떤 필드를 선택 할 수 있는지, 어떤 종류의 객체를 반환할 수 있는지, 하위객체에서 사용할 수 있는 필드는 무엇인지, 이것이 바로 스키마가 필요한 이유 입니다.
모든 GraphQL 서비스는 해당 서비스에서 쿼리 가능한 데이터들을 완벽하게 설명하는 타입들을 정의하고, 쿼리가 들어오면 해당 스키마에 대해 유효성이 검사된 후 실행됩니다.

객체 타입과 필드
=
GraphQL 스키마의 가장 기본적인 구성 요소는 객체 타입입니다. 객체 타입은 서비스에서 가져올 수 있는 객체의 종류와 필드를 나타냅니다. GraphQL 스키마 언어에서는 다음과 같이 표현할 수 있습니다.
~~~
type Character{
	name:String!
	appearsIn: [E


https://graphql-kr.github.io/learn/schema/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ2ODkxNjQ3MywtOTI2OTM1NTQzXX0=
-->