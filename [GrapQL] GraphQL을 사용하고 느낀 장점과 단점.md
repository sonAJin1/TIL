Graphql 장점과 단점 그리고 아쉬웠던 점
=

Graphql을 사용해서 작업했던 프로젝트가 마무리되면서 graphql을 써봤을 때의 장점, 그리고 아쉬웠던 점들을 정리하려고 한다.

**작업환경**
~~~

Android Studio 3.3.1
Apollo 2.5.0 darwin-x64 node-v11.8.0

Gradle 설치 버전 : 
implementation 'com.apollographql.apollo:apollo-runtime:1.0.0-alpha5'  
implementation 'com.apollographql.apollo:apollo-android-support:1.0.0-alpha5'  
implementation 'com.apollographql.apollo:apollo-rx2-support:1.0.0-alpha5'

~~~

장점
-
서버쪽에서는 endpoint가 하나이기 때문에 **한 번에 여러 클라이언트들의 요청에 대응할 수 있고,** 프론트 쪽에서 필요한 정보만 서버에 요청할 수 있다 보니 여러 쿼리들을 한 번에 호출하는 등 **필요한 요청에 따라서 원하는 대로 쿼리를 커스텀 해서 사용할 수 있어, 프론트의 자유도가 높다는 장점이 있다.**

단점
-
하지만 프론트에서 쿼리를 직접 작성해야 하기 때문에 서버 쪽 스키마를 제대로 알고 있어야 하고 어떤 식으로 쿼리문을 작성해야 할지 고민해야 하기 때문에 초기 설계에서 고려해야 할 점들이 많아진다.

GraphQL의 특징인 Endpoint가 하나이기 때문에 생기는 단점도 있다. 처음 서버쪽에서 스키마 구조를 잡을 때 프론트 개발자들과 충분히 커뮤니케이션이 이루어져야하고 프론트쪽 개발자들끼리도 각자의 단말의 특성상 필요한 정보가 다를 수 있기 때문에 이에 대해서 충분히 논의가 되어야 한다는 점에서 초기 비용이 많이 든다는 단점이 있다.

서버 쪽에서 만든 스키마 파일을 프론트도 가지고 있어야 하는데, 이 파일은 서버 쪽 스키마가 변경되는 경우 새로 다운받아서 build 해줘야 한다. 이때 기존에 만들어둔 쿼리문에서 변경된 스키마의 영향을 받는 경우 아래와 같은 build에러가 나는데, 어디서 에러가 나는지 알려주지 않기때문에 일일히 찾아야하는 번거로움이 있다. 
~~~
Process 'command '/Users/[projectName]/app/.gradle/nodejs/node-v6.7.0-darwin-x64/bin/node'' finished with non-zero exit value 1
~~~
위의 에러가 나는 경우는 대체로 스키마와 쿼리문의 구조가 일치하지 않는 경우와, 쿼리문에 이름을 생략했을 경우 두가지였다.


아쉬웠던 점
-
이번 프로젝트에서 Union type의 스키마가 많아서 Fragment를 많이 이용해서 query문을 만들었다. 그런데 같은 구조인 Union type의 스키마들을 호출하는 화면이 많았고, Android에서 GrphqQL 파일을 기능별로 나눠서 따로 생성해서 사용하다보니 비슷한 구조의 Fragment가 여러 쿼리문 파일에 여러번 반복되어 만들어졌다. Fragment는 다양한 type에 대응하는 query문을 만드는 역할도 하지만 중복을 피하게하는 역할 또한 있는데, 후자의 장점을 전혀 사용하지 못하는 결과가 나타났다. 

결국 아직 GraphQL의 쿼리 문법이 아직 익숙치 않은 것들이 많고, 그러다보니 비효율적으로 구조를 짜고있는 것 같다. 다음에는 쿼리문을 더 효율적으로 구성 할 수 있는 방법에 초점을 맞춰서 진행해야겠다.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ3Nzg5MTU4MF19
-->