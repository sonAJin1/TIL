새 테스트 추가
=
로컬 단위 테스트 또는 계측 테스트를 생성하려면 다음 단계에 따라 특정 클래스 또는 메서드에 대한 새 테스트를 생성합니다.

1.  테스트할 코드를 포함하는 Java 파일을 엽니다. ![test code](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.18.00.png?raw=true)

2.  테스트하려는 클래스 또는 메서드를 클릭한 후 `맥:⇧⌘T` `윈도우: Ctrl+Shift+T`를 누릅니다.

3.  나타나는 메뉴에서  **Create New Test**를 클릭합니다.![create new test](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.18.16.png?raw=true)

4.  **Create Test**  대화상자에서 필드를 편집하고 테스트하고 싶은 메서드를 선택한 후  **OK**를 클릭합니다.![enter image description here](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.18.28.png?raw=true)

5.  **Choose Destination Directory**  대화상자에서 생성하려는 테스트 유형에 해당하는 소스 세트를 클릭합니다. 에뮬레이터나 디바이스에서 테스트를 해야하는 경우 **androidTest**, 로컬 단위 테스트를 생성하려는 경우  **test**를 클릭합니다. ![](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.18.41.png?raw=true)

위의 단계를 거치고 나면 **test 폴더** 아래에 `CalculatorTest` 라는 파일이 생성된 것을 볼 수 있습니다. 저는 계산이 잘 되는지만 확인하고 싶기 때문에 화면까지 함께 확인할 수 있는 `androidTest`가 아니라 `test`에 파일을 생성했습니다.
![](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.44.21.png?raw=true)


아래처럼 테스트를 선택한 메소드들이 생성 된 것을 확인할 수 있습니다.

![enter image description here](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.19.41.png?raw=true)


로컬 단위 테스트
=

위의 과정으로 테스트 파일을 생성 후, 각 메소드들이 잘 실행되는지 테스트 해보겠습니다.  `add()`는 맞는 결과값이 출력되게 `minus()`는 틀린 결과 값이 출력되게 구성하여 테스트를 실행할 수 있습니다. (`CalculatorTest`를 우클릭하여 run)

![](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.52.14.png?raw=true)

![](https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202019-03-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.49.40.png?raw=true)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODM5Mjc0OTFdfQ==
-->