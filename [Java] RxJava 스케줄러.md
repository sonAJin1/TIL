Scheduler
=

스케줄러는 해당 옵저버블, 오퍼레이터, 서브스크라이버를 어떤 스레드에서 수행할지 결정하는 것입니다. 스케줄러가 어떤 부분에 맞게 되는지는 `subscribeOn`과 `obserbeOn`으로 지정합니다.

-	**subscribeOn :** 구독할 때 사용할 스레드를 지정
-	**obserbeOn :** observable이 아이템을 전파할 때 사용할 스레드 지정


Scheduler 목록
=

스케줄러는 RxJava가 제공하는 것과 RxAndroid가 제공하는 스케줄러가 있습니다.

**RxJava Scheduler :**

-	**Schedulers.computation()** 간단한 연산이나 콜백처리를 위해서 사용. I/O처리를 여기서 처리하면 안됨
-	**Schedulers.from(executor)** 특정 executor(집행자)로 사용
-	**Schedulers.immediate()** 현재 스레드에서 즉시 수행
-	**Schedulers.io()** 동기 I/O를 별도로 처리시켜 비동기 효율을 얻기위한 스케줄러 자체적인 스레드 풀에 의존
-	**Schedulers.newThread()** 항상 새로운 스레드를 만드는 스케줄러
-	**Schedulers.trampoline()** 새로운 스레드를 생성하지 않고, 현재 스레드에서 큐에 있는 일이 끝나면 다음 작업을 순차적으로 실행

일부 operator들은 자체적으로 어떤 스케줄러를 사용할지 지정합니다. 예를들어 `buffer`라는 operator는 `Schedulers.computation()`에 의존하며 `repeat`은 `Schedulers.trampoline()`을 사용합니다.


**RxAndroid Scheduler :**

-	**AndroidSchedulers.mainThread()** 안드로이드의 UI스레드에서 동작
-	**HandlerScheduler.from(handler)** 특정 핸들러에 의존하여 동작

보통은 RxAndroid가 제공하는 `AndroidSchedulers.mainThread()`와 RxJava가 제공하는 `Scheduler.io()`를 조합해서 `Scheduler.io()`에서 수행한 결과를 `AndroidSchedulers.mainThread()`에서 받아 UI에 반영하는 패턴등이 일반적으로 쓰입니다.


----
참고 : https://academy.realm.io/kr/posts/create-a-reactive-app-with-rxandroid-4/
http://blog.weirdx.io/post/26576
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU3MDc0MTkwNl19
-->