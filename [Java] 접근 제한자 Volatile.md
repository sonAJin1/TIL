
Java Volatile 이란
=

-   Java 변수를 Main Memory에 저장하겠다는 것을 명시하는 것
-   매번 변수의 값을 Read할 때마다 CPU cache에 저장된 값이 아닌 Main Memory에서 읽는 것
-   또한 변수의 값을 Write할 때마다 Main Memory에 까지 작성하는 것

  

필요한 이유
=

volatile  변수를 사용하고 있지 않는 MultiThread 어플리케이션에서는 Task를 수행하는 동안 **성능향상**을 위해 Main Memory에서 읽은 변수 값을 CPU Cache에 저장하게 됩니다.

만약에 Multi Thread환경에서  `**Thread가 변수 값을 읽어올 때**`  각각의 CPU Cache에 저장된 값이 다르기 때문에  `**변수 값 불일치 문제**`가 발생하게 됩니다.

volatile이 적합한 경우
=
-   Multi Thread 환경에서 하나의 Thread만 read & write하고 나머지 Thread가 read하는 상황에서 `가장 최신의 값을 보장`합니다.
-   하나의 Thread가 아닌 여러 Thread가 write하는 상황에서는 적합하지 않습니다.
-   여러 Thread가 write하는 상황이라면?
    -   `synchronized`를 통해 변수 read & write의 원자성(atomic)을 보장해야 합니다.

volatile이 성능에 주는 영향
=

-   `volatile`는 변수의 read와 write를 Main Memory에서 진행하게 됩니다.
-   `CPU Cache`보다  `Main Memory`가 비용이 더 크기 때문에  `변수 값 일치`을 보장해야 하는 경우에만  `volatile`  사용하는 것이 좋습니다.

  

  

출처 : https://nesoy.github.io/articles/2018-06/Java-volatile
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjgyODc1MDBdfQ==
-->