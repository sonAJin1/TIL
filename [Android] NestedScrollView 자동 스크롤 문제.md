NestedScrollView 자동으로 스크롤되는 문제
=

안드로이드 레이아웃을 만지다 보면 ScrollView 안에 ScrollView(RecyclerView같은)를 넣어야 할 때가 있는데, 이럴 때 쓰는게 바로  [NestedScrollView](https://developer.android.com/reference/android/support/v4/widget/NestedScrollView.html)이다. 그런데 경우에 따라서 안에 넣어둔 또 다른 ScrollView에 포커스가 가버리면서 이 NestedScrollView가 보여질 때 자기 멋대로 밑으로 스크롤이 내려갈 때가 있다. 이 포커스를 제거하려면 NestedScrollView 가 감싸고 있는 ViewGroup에 `android:descendantFocusability="blocksDescendants"` 를 추가해주면 해결할 수 있다.

~~~
<android.support.v4.widget.NestedScrollView      
	android:layout_width="match_parent"      
	android:layout_height="match_parent">    
	 
	<ViewGroup        
	android:descendantFocusability="blocksDescendants"        
	android:layout_width="match_parent"        
	android:layout_height="wrap_content"/> 
	
</android.support.v4.widget.NestedScrollView>
~~~
descendantFocusability 속성은 **ViewGroup 내에서 포커스를 맞출 뷰를 찾을 때 ViewGroup과 그의 하위 뷰의 관계를 설정하는 역할**이다.

이 중 위 예제에서 설정한 blocksDescendants는 해당 뷰그룹의 하위 뷰가 포커스를 받지 못하게 하는 옵션으로, 위에서 말했던 내부의 다른 스크롤뷰가 포커스를 받아가는 일이 없도록 해준다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0NDk1OTk5XX0=
-->