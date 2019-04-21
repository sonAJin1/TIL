Android에서 Union 타입의 데이터 가져오기
=
 

Android에서 Apollo를 이용하여 GraphQL을 적용하는 중 Union타입의 데이터가 받아서 꺼내 쓰기에 불편하다는 것을 발견했다.
다른 타입의 데이터들은 `Data.id` 이런식으로 꺼내 쓰는게 가능한데, Union타입은 `Data { id="01', name="yam"}` 구조인데도 `Data.id` 처럼 꺼내쓰는게 불가능했다.
어떻게 해야 다른 타입들 처럼 데이터를 바로 꺼내서 쓸 수 있을까 고민하던 중 **Fragment를 사용하여 해결**되었다.

아래 예제의 Product 와 Content가 Union 타입이었을 때, 상단의 수정전 쿼리문을 하단 처럼 fragment로 따로 뺀 형식으로 수정했다.


~~~


** 수정전 **

query feed{
  feed{
	id
	title
	data{
		on Product
		on Content
		}
	}
}

========================================		 


** 수정후 **

query feed{
  feed{
    id
    title
    data {
       ...productData
       ...contentData
    }
  }
}

fragment productData on Prodcut {
	id
	title
	summary
	type
	img{
		url
		width
		height
	}
}
fragment contentData on Content {
	id
	title
	summary
	type
	img{
		url
		width
		height
	}
}
~~~

Fragment
=
**Fragment는 재사용이 뛰어난 Query문의 파편의 역할을 한다.**
또한 query type이 union 혹은 interface와 같이 여러 type이 있을수 있을때 Fragment의 타입 질의기능을 활용하여 특정 타입에만 적용되는 Query문을 작성할수 있다.


---
**작업환경**
~~~

Android Studio 3.3.1
Apollo 2.5.0 darwin-x64 node-v11.8.0

Gradle 설치 버전 : 
implementation 'com.apollographql.apollo:apollo-runtime:1.0.0-alpha5'  
implementation 'com.apollographql.apollo:apollo-android-support:1.0.0-alpha5'  
implementation 'com.apollographql.apollo:apollo-rx2-support:1.0.0-alpha5'

~~~

---
참고: [https://vomvoru.github.io/blog/mutation-and-fragment-of-GraphQL/](https://vomvoru.github.io/blog/mutation-and-fragment-of-GraphQL/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNjkxNDQwNDYsMTgxNTc1MDEyMl19
-->