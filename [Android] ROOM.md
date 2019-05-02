ROOM이란?
=

**ROOM은 ORM(Object Relational Mapping) 라이브러리**입니다. 쉽게 말해 ROOM은 데이터베이스의 객체를 자바 or코틀린 객체로 매핑해주는것 입니다. ROOM은 SQLite의 추상레이어 위에 제공하고 있으며 SQLite의 모든 기능을 제공하면서 편한 데이터베이스의 접근을 허용합니다  


ROOM과 SQLite의 차이점
=
1. SQLite 경우 쿼리에 대한 에러를 컴파일에 확인하는것이 없지만 **ROOM 에서는 컴파일 도중 SQL에 대한 유효성을 검사 할 수 있습니다.**

  

2. **Schema**가 변경이 될경우 SQL쿼리를 수동으로 업데이트 해야하지만 **ROOM**의 경우는 쉽게 해결이 가능합니다.

  

3. SQLite 경우 Java데이터 객체를 변경하기위해 많은 상용구 코드(Boiler Plate code)를 사용해야하지만 **ROOM의 경우 ORM라이브러리가 상용구 코드(Boiler Plate code) 없이 매핑 가능합니다.**

>BoilerPlateCode : 수정하지 않거나 최소한의 수정만을 거쳐 여러곳에 필수적으로 사용되는 코드

4. **ROOM의 경우 LiveData와 RxJava를 위한  Observation 으로 생성하여 동작할 수 있지만** SQLite는 그렇지 않습니다.

  
  ROOM의 세가지 구성 요소
  =
  **ROOM**에는 크게 3가지 구성요소(**Database, Entity, Dao)** 가 있습니다.

-  **Database**  : RoomDatabase를 확장하는 추상 클래스입니다. 여기에는 데이터베이스 소유자가 포함되며 기본 연결에 대한 기본 액세스 지점으로 사용됩니다.

-  **Entity** : Database 내의 테이블을 뜻합니다.

-  **Dao** : 데이터베이스에 엑세스하는데 사용되는 메소드들을 갖고있습니다. select, insert, delete, join...등 데이터를 쓰거나 읽을때 사용합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile28.uf.tistory.com%2Fimage%2F99D89F395C1B02EC247175)
  

---
참조: https://namget.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-ROOM-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%BD%94%EB%A3%A8%ED%8B%B4

https://medium.com/mindorks/android-architecture-components-room-and-kotlin-f7b725c8d1d
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyMjAxODI5Nl19
-->