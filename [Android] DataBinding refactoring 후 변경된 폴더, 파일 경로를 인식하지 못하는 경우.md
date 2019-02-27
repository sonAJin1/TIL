---


---

<h1 id="android-databinding-refactoring-후-변경된-폴더-파일-경로를-인식하지-못하는-경우">Android DataBinding refactoring 후 변경된 폴더, 파일 경로를 인식하지 못하는 경우</h1>
<p>Android Studio에서 DataBinding을 사용하면서 파일과 폴더의 위치를 바꿨는데 Android Studio가 이를 인식하지 못하고 계속 전에 있던 경로로 나타나는 경우가 있었다.</p>
<p>시도 했었던 방법은 크게 2가지로 정리할 수 있다</p>
<ol>
<li>Gradle에서 databinding enabled = false 로 변경 후 clean project 하고 다시 true로 변경</li>
<li>위치 변경할 파일들을 삭제하고 clean project, rebuild project 후에 다시 파일 만들기 (이때 DataBinderMapperImpl에서 오류가 나서 결국 git으로 되돌아왔다)</li>
</ol>
<p>하지만 나에게는 모두 소용이 없었다ㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠ</p>
<p>그래서 다시 <strong>Android Studio가 인식하는 상태로 파일 위치를 되돌린 후에<br>
clean project, rebuild project 후에 내가 원하는 폴더로 이동</strong>시켰더니 바뀐 위치를 제대로 인식했다…</p>
<p>생각보다 간단히 해결될 수 있는 문제 였는데!<br>
역시 삽질의 연속이다</p>

