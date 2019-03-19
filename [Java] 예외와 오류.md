예외와 오류
=
**오류(Error)** 는 시스템이 비정상적인 상황이 생겼을 때 발생한다. 이는 시스템 레벨에서 발생하기 때문에 심각한 수준의 오류이다. 따라서 개발자가 미리 예측하여 처리할 수 없기 때문에, 애플리케이션에서 오류에 대한 처리를 신경 쓰지 않아도 된다. 

오류가 시스템 레벨에서 발생한다면, **예외(Exception)** 는 개발자가 구현한 로직에서 발생한다. **예외는 발생할 상황을 미리 예측하여 처리할 수 있다.** 고로 예외는 개발자가 처리할 수 있기 때문에 예외를 구분하고 그에 따른 처리 방법을 명확히 알고 적용하는 것이 중요하다.

예외를 전달하는 방법
=

예외나 오류를 전달하는 방법은 크게 2 가지로 나눌 수 있다. **'반환값으로 알린다'** 와 **'실패하면 점프한다'** '반환값으로 알린다' 전략에는 반환값을 확인하는 것을 잊어버려서 실패를 놓칠 수 있다는 문제가 있다. 그래서 모든 실패를 잡을 수 있는 '실패하면 전달한다'는 전략이 오랜 시간 연구되어 왔다. 이것이 지금의 Java, C++, Python, Ruby 등 많은 언어가 지원하고 있는 **예외 처리 구조이다.**


예외 클래스
=
![예외 클래스의 구조](http://www.nextree.co.kr/content/images/2016/09/Exception-Class.png)

모든 예외 클래스는 Throwable 클래스를 상속받고 있으며, Throwable은 최상위 클래스 Object의 자식 클래스이다. Throwable을 상속받는 클래스는 Error와 Execption이 있다.

Exception은 수많은 자식클래스를 가지고 있다. **그 중 RuntimeException은 CheckedException과 UncheckedException을 구분하는 기준이다** Exception의 자식 클래스 중 RuntimeException을 제외한 모든 클래스는 CheckedException이며, RuntimeException과 그 자식 클래스들을 Unchecked Exception이라 부른다. 

CheckedException과 Unchecked(Runtime) Exception
=
| | Checked Exception | UnChecked Exception |
|:--:|:--:|:--:|
| 처리여부 | 반드시 예외처리를 해야함 | 강제하지 않음 |
|확인시점 | 컴파일 단계 | 실행 단계 |
|예외발생시 트랜잭션 처리 | roll-back 하지 않음 | roll-back 함 |
|대표 예외 | Exception의 상속받는 하위클래스 중 Runtime Exception을 제외한 모든 예외 (IOEception, SQLException) | RuntimeException 하위 예외 (NullPointerException, IllegalArgumentExcpetion, IndexOutOfBoundException, SystemException) |


Checked Exception과 Unchecked Exception의 가장 명확한 구분은 **'꼭 처리를 해야하느냐'** 이다. Checked Exception이 발생할 가능성이 있는 메소드라면 반드시 로직을 try/catch로 감싸거나 throw로 던져서 처리해야한다. 반면에 Unchecked Exception은 명시적인 예외처리를 하지 않아도 된다. 이 예외는 피할 수 있지만 개발자가 부주의해서 발생하는 경우가 대부분이고, 미리 예측하지 못했던 상황에서 발생하는 예외가 아니기 때문에 굳이 로직으로 처리 할 필요가 없다. 

기본적으로 Checked Exception은 예외가 발생하면 트랜잭션을 roll-back하지 않고 예외를 던져준다. 하지만 Unchecked Exception은 예외 발생시 트랜잭션을 roll-back 해준다.
roll-back이 되는 범위가 달라지기 때문에 개발자가 이를 인지하지 못하면, 실행결과가 맞지 않거나 예상치 못한 예외가 발생할 수 있다. 그러므로 이를 인지하고 트랜잭션을 적용시킬 때 전파방식과 롤백규칙 등을 적절히 사용해야한다.

예외처리 방법
=
예외처리 방법에는 크게 3가지가 있다.

-	**예외 복구:** 다른 작업 흐름으로 유도
-	**예외처리 회피:** 처리하지 않고 호출한 쪽으로 throw
-	**예외 전환:** 명확한 의미의 예외로 전환 후 throw

**예외 복구**의 핵심은 예외가 발생하여도 애플리케이션은 정상적인 흐름으로 진행된다는 것이다. **예외처리 회피** 는 신중해야하는 로직이다. 호출한 쪽에서 다시 예외를 받아 처리하도록 하거나, 예외를 던지는 것이 최선의 방법일 때만 진행한다. **예외 전환** 은 호출한 쪽에서 예외를 받아서 처리할 때 좀 더 명확하게 인지할 수 있도록 돕기 위한 방법이다. 이를 Unchecked Exception으로 전환하여 다른 계층에서 일일이 예외를 선언할 필요가 없도록 할 수 있다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzIzNzgxOTQzXX0=
-->