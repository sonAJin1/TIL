리액트 프로그래밍의 개념
=
리액티브 프로그램은 주변의 환경과 끊임없이 상호작용을 하는데 프로그램이 주도하는 것이 아니라 **환경이 변하면 이벤트를 받아 동작합니다.** 상호작용 프로그램은 자신의 속도에 맞춰 일하고 대부분 통신을 담당합니다. 반면에 리액티브 프로그램은 외부 요구에 끊임없이 반응하고 처리합니다.


명령형 프로그래밍 vs 리액티브 프로그래밍
=
-	**명령형 프로그래밍: ** 작성된 코드가 정해진 순서대로 실행됨
-	**리액티브 프로그래밍:** 데이터 흐름을 먼저 정의하고 데이터가 변경되었을 때 연관되는 함수나 수식이 업데이트 되는 방식


자바와 리액티브 프로그래밍의 관계
=
-	**기존 pull 방식의 개념을 push 방식으로 바꿈:** 
	-	**pull :** 주제객체가 구독객체에게 상태를 보내는 방식
	-	**push :** 구독 객체가 주제 객체에게서 상태를 요청하는 방식
- **함수형 프로그래밍의 지원을 받음 :** 함수형 프로그래밍은 Side effect가 없다. 콜백이나 옵저버 패턴이 스레드에 안전하지 않은 이유는 같은 자원에 여러 스레드가 경쟁조건에 빠지게 되었을 때 알 수 없는 결과가 나오기 때문이다. (이를 Side effect라고 한다) 함수형 프로그래밍은 Side Effect가 없는 순수 함수를 지향하기 때문에 스레드에 안전하다.



Observable
=
Observable은 데이터 흐름에 맞게 알림을 보내 구독자가 데이터를 처리할 수 있도록한다. 안드로이드에서 버튼을 클릭하면 이벤트를 받을 수 있게 하는 OnClickListener가 대표적인 옵저버 패턴의 예라고 할 수 있다.

RxJava에서 Observable은 세가지를 구독자에게 전달한다.

-	**onNext :** Observable이 데이터의 발행을 알린다.
-	**onComplete :** 모든 데이터가 발행이 완료 되었음을 알린다. 그럼으로 더 이상의 onNext는 발생하지 않으며, 마지막에 한번만 호출된다.
-	**onError :** Observable에서 어떤 이유로 에러가 발생했음을 알린다. onError 이벤트가 발생하면 onNext, onComplete 이벤트가 발생하지 않는다. 즉, Observable의 실행을 종료한다.



## 1. Do Operator 

Observable에서 특정 이벤트가 발생할 때 호출할 콜백을 등록 할 수 있습니다. 이러한 콜백은 Observable 에 종속된 정상적인 알림들과는 별도로 호출됩니다,

- **doOnCompleted :** 실행 결과 값이 나올때 마다 호출 콜백을 설정할 수 있습니다. onNext의 다양한 Notification 단독 매개 변수로 
- **doOnNext :**  consumer을 취해서 아이템들이 실시간으로 보여주는 값에 대해서 뭔가를 할 수 있게 해준다.
- **doOnEach :**
- **doOnError :** 결과 Observable이 비정상적으로 종료되면 호출 될 Action을 등록하고 onError를 호출합니다. 이 액션에는, 에러를 나타내는 Throwable가 건네받습니다.
- **doOnSubscribe :** 관찰자가 Observable의 결과를 받을 때마다 호출 될 Action을 등록합니다.
- **doOnTerminate :** Observable이 정상적으로 종료했는지 오류가 있든간에 종료되기 직전에 호출 될 Action을 등록합니다.
- **doOnUnSubscribe :** 관찰자가 Observable에서 구독을 취소 할 때마다 호출 될 Action을 등록합니다.
- **finallyDo :** Observable이 정상적으로 종료했는지 또는 오류가 발생했는지에 관계없이 종료 될 직후에 호출 될 Action을 등록합니다. (RxJava 1.1.1 이후로 사용되지 않음)

출처 : http://reactivex.io/documentation/operators.html#utility

## 2. Single Class

Observable 클래스는 데이터를 1개 이상 발행할 수 있지만 Single 클래스는 **1개의 데이터만 발행하도록 한정합니다.** 서버 API를 호출할 때 유용합니다.

Single의 가장 큰 특징은 데이터가 발행과 동시에 종료 된다는 점입니다. 그래서 Single 클래스의 라이프 사이클은 onSuccess와 onError 함수로 구성됩니다.

출처 : https://www.charlezz.com/?p=189
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzMTY1MzA4NV19
-->