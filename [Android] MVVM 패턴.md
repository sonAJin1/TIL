


<h1 id="mvvm에서의-view와-viewmodel">MVVM에서의 View와 ViewModel</h1>
<ul>
<li>
<p>View는 화면에 표시되는 레이아웃에 대해 관여합니다. 기본적으로 비지니스 모델에서 베제하지만 UI에 관련된 로직들을 수행합니다.</p>
</li>
<li>
<p>ViewModel은 View에 연결할 데이터와 명령으로 구현되어있으며 변경 알림을 통해서 뷰에게 상태 변화를 전달합니다.</p>
</li>
<li>
<p>전달받은 상태변화를 화면에 적용할지는 View에서 결정하게 합니다</p>
</li>
<li>
<p>명령은 UI를 통해서 동작하도록 합니다</p>
</li>
</ul>
<h1 id="view와-viewmodel의-관계">View와 ViewModel의 관계</h1>
<p><img src="https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/2019_03_01_mvvm_01.JPG" alt="enter image description here"></p>
<ul>
<li>
<p>ViewModel은 Model은 알지만 View는 알지 못합니다.</p>
</li>
<li>
<p>View는 ViewModel은 알지만 Model을 알 수 없습니다</p>
</li>
<li>
<p>View는 ViewModel을 옵저빙 하고 있다가 상태가 변화하면 화면을 갱신해야 합니다.</p>
</li>
</ul>
<h1 id="databinding--view와-viewmodel의-독립">DataBinding : View와 ViewModel의 독립</h1>
<p><img src="https://github.com/sonAJin1/sonAJin1.github.io/blob/master/assets/img/2019_03_01_mvvm_02.JPG" alt="enter image description here"></p>
<ul>
<li>
<p>DataBinding은 View와 ViewModel 사이의 데이터와 명령을 연결해주어 각자의 존재를 명확하게 알지 못해도 다양한 인터랙션을 할 수 있게 도와주는 역할을 합니다.</p>
</li>
<li>
<p>DataBinding을 통해서 View와 ViewModel은 독립성을 더 높힐 수 있습니다</p>
</li>
</ul>

