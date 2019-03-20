ADB를 사용하여 안드로이드 무선 디버깅
=
안드로이드 개발 툴에서 USB연결 없이 와이파이 연결을 통해서 무선으로 디버깅하는 것이 가능하다.
하지만 컴퓨터를 켤때마다 한번은 USB를 연결한 상태에서 세팅을 해야하기 때문에 USB 케이블은 가지고 있어야한다.

>**테스트 환경 :** 
>
>MacOS : 10.14.3 Mojave
>Android Studio : 3.3.1
>Android SDK Platform-Tools : 28.0.1 
>
>Galaxy S7 (Android 8.0 Oreo)

---
**무선 연결 방법 :**

1. 개발용 맥과 단말기는 동일한 네트워크에 접속되어 있어야 한다. (같은 아이피 대역 안에 있어야 함)
2. 단말기를 맥에 USB로 연결한다.
3. 터미널을 열어 Android Platform-tools이 설치된 폴더로 이동한다. `/Users/*username*/Library/Android/sdk/platform-tools`
4.  터미널에서 ADB를 사용하여 단말기가 연결 되어 있는지 확인한다. `$ adb devices`
5. 터미널에서 ADB를 네트워크 모드로 변경한다. (이때 단말기는 USB로 연결되어 있어야한다) `$ adb tcpip 5555`
6. 단말기에 할당된 IP를 확인한다. (설정 - wifi - 우측 상단 클릭 - 고급 - IP 주소 의 숫자가 내부아이피)
7. USB를 맥에서 분리
8. ADB에서 단말기로 무선 연결한다. `$ adb connect [단말기 IP]`

---
**command not found: adb 오류 해결 방법:**

위의 오류는 환경 변수를 설정하지 않아서 발생하는 오류이다. macOS에서 환경변수는  **.bash_profile**  파일에 지정되어있다.

1. 파일 확인 `$ ls -l -a ~/.bash_profile` 
2. 'No such file or directory' 라는 오류가 나오면 파일 생성 `touch -c ~/.bash_profile`
3. 텍스트 편집기 열기 `$ open -e ~/.bash_profile`
4. 파일에 내용 추가 (스튜디오 버전 별로 경로가 다를 수 있으니 확인 후 진행할 것)  `$ export PATH=${PATH}:/Users/*username*/library/android/sdk/tools:${PATH}:/Users/*username*/library/android/sdk/platform-tools `
5. 저장하고 닫은 후 새로고침을 하면 환경 변수에 등록된다. `$ source ~/bash_profile`
6. `$ adb version`을 입력하고 버전이 출력되면 성공

---
참고:
https://wingsnote.com/91
https://seonift.github.io/2018/02/05/macOS-%ED%84%B0%EB%AF%B8%EB%84%90%EC%97%90%EC%84%9C-adb-%EC%8B%A4%ED%96%89-%EC%8B%9C-%EB%82%98%EC%98%A4%EB%8A%94-command-not-found-adb-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95/
https://hancho1111.tistory.com/87
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkyMzY3NzY1NV19
-->