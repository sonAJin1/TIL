GraphQL이란?
=
GraphQL은 REST같은 API 디자인에 관한 새로운 관점의 기술입니다.
REST API는 데이터가 커지면서 데이터 쿼리가 복잡 해짐에 따라 시간과 계산 측면에서 비용이 많이 듭니다.
GraphQL은 이런 REST API의 단점을 보안하기 위하여 고안된 API 를위한 쿼리 언어입니다. 단일 플랫폼에 한정되지 않고 **Android, iOS 또는 웹을 포함한 모든 유형의 클라이언트에서 작동합니다** . 서버와 클라이언트 사이에 있으며 데이터를 더욱 최적화 된 방식으로 쿼리하는 데 도움이됩니다.

**주요 이점 :**

-   **클라이언트 주도형으로 필요한 것만 얻을 수 있습니다.** 클라이언트는 서버에서 필요한 데이터를 호출할 수 있으며, 어떤 유형의 응답을 받을지 정의합니다
- **여러 건의 호출을 피할 수 있습니다.** REST API의 경우 여러 end point를 유지 관리해야합니다. 예를 들어 사용자 의 "ID" 와 사용자 세부 정보 를 얻는 하나의 엔드 포인트는 세부 정보에 대한 두 번의 호출을 요구합니다.  graphQL에서는 이러한 단점을 단일 쿼리로 줄여 해결할 수 있습니다.  
![REST API](sonAJin1.github.io/assets/img/2019_03_04_graphql_02.png)
REST API를 사용했을 때는 피자를 주문한 다음 식료품을 주문하고 드라이 클리닝업자에게 옷을 가져다주는 것과 같습니다. 
![GraphQL](sonAJin1.github.io/assets/img/2019_03_04_graphql_03.png)
반면에 GraphQL은 개인 비서가있는 것과 같습니다. 내가 원하는 것을 한번 호출 하는 것으로 해결할 수 있습니다 ( "내 드라이 클리닝, 큰 피자와 두 알의 계란을 사주세요" )
- **모든 언어로 작성할 수 있습니다.** JavaScript와 같은 특정 프로그래밍 언어 구문에 의존 하지 않고 GraphQL자체의 간단한 "GraphQL 스키마 언어"를 사용합니다. 이것은 쿼리 언어와 유사하며, 언어에 구애받지 않는 방식으로 GraphQL 스키마에 관해 이야기 할 수 있습니다.

참고: https://medium.freecodecamp.org/so-whats-this-graphql-thing-i-keep-hearing-about-baf4d36c20cf
https://medium.com/mindorks/what-is-graphql-and-using-it-on-android-ab8e493abdd7
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NTQzOTkxNzAsLTE5MDM1MTksLTIwOT
I3Mzc5ODAsLTE2NDMxMTI2NzEsMTU3Mzg2NzAzMSwtMzA0OTkx
NDg0LC01ODU2MjMxMjEsLTIwODg3NDY2MTJdfQ==
-->