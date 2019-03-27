안드로이드 테스트 종류
=
![안드로이드 테스트 종류](https://t1.daumcdn.net/cfile/tistory/99D2D3415BB70D7B29)

1. **Unit 테스트:** 일반적으로 코드의 유닛 단위(메소드, 클래스, 컴포넌트)의 기능을 실행하는 방식
	-	관련 툴 : JUnit, Mockito, PowerMock

2. **UI 테스트:** 사용자 인터랙션 (버튼 클릭, 텍스트 입력 등)을 평가
	-	관련 툴 : Espresso, UIAutomator, Robotium, Calabash, Robolectric


Android Studio 앱테스트 
=
 Android Studio는 테스트 작업을 간단하게 수행할 수 있도록 설계되었습니다. 
 - **JUnit :** 로컬 JVM에서 실행되는 계측 테스트를 설정할 수 있습니다.
 - **Mockito :** 로컬 단위 테스트에서 Android API 호출을 테스트 할 수 있습니다. 
 - **Espresso :** 계측 테스트에서 사용자 상호작용을 시험할 수 있습니다.
 - **UI Automator :** 이를 통합하여 테스트 기능을 확장할 수 있습니다. 
 - **Espresso Test Recorder :** Espresso 테스트를 자동으로 생성할 수 있습니다.


테스트 유형 및 위치
=
테스트 코드의 위치는 작성하는 테스트의 유형에 따라 결정됩니다. Android Studio에서는  두 가지 테스트 유형에 대한 소스 코드 디렉토리를 제공합니다.

**로컬 단위 테스트 :**
위치:  `module-name/src/test/java/`.

컴퓨터의 로컬 JVM(Java Virtual Machine)에서 실행되는 테스트입니다. 하드웨어 또는 에뮬레이터가 필요없는 테스트가 진행되는 곳입니다. 테스트에 Android 프레임워크 종속성이 없거나 Android 프레임워크 종속성에 대한 모의 객체를 생성할 수 있는 경우 이 테스트를 사용하면 실행 시간을 최소화할 수 있습니다.

런타임에 이 테스트는 `final`  한정자가 삭제된 수정된 버전의  `android.jar`에 대해 실행됩니다. 여기서는 Mockito와 같이 흔히 사용되는 모의 라이브러리를 사용할 수 있습니다.

---
**계측 테스트 :**
위치:  `module-name/src/androidTest/java/`.

하드웨어 기기나 에뮬레이터에서 실행되는 테스트입니다. 이 테스트에서는  `Instrumentation`  API에 액세스할 수 있으며, 테스트하는 앱의  `Context`  와 같은 정보에 대한 액세스 권한을 개발자에게 제공합니다. 사용자 상호작용을 자동화하는 통합 및 기능적 UI 테스트를 작성하거나 테스트에 모의 객체가 충족할 수 없는 Android 종속성이 있는 경우 이 테스트를 사용합니다.

계측 테스트는 APK(앱 APK와는 별개임)로 빌드되므로 자체  `AndroidManifest.xml` 파일을 가져야 합니다. Gradle이 빌드 과정에서 이 파일을 자동으로 생성하게 됩니다. `minSdkVersion`에 다른 값을 지정하거나 테스트 전용 실행 리스너를 등록하는 등과 같이 필요한 경우 자체 매니페스트 파일을 추가할 수 있습니다. 앱을 빌드하면 Gradle이 여러 매니페스트 파일을 하나의 매니페스트 파일로 병합합니다.



-----
참고 : https://black-jin0427.tistory.com/107
https://alexzh.com/2016/03/24/android-testing-unit-testing/
https://developer.android.com/studio/test?hl=ko
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTU1MDU4N119
-->