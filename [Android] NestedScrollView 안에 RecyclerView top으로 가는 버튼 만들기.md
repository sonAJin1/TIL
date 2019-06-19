NestedScrollView 안에 RecyclerView
=

NestedScrollView안에 있는 RecyclerView 스크롤을 Top으로 이동시키는 작업을 하는데 아무리 RecyclerView의 스크롤을 이동시키려고 해도 작동하지 않았다.
NestedScrollView 스크롤을 이동시키는 방법으로 문제 해결... 왜 NestedScrollView로 감싸져있는걸 잊고있었을까ㅠㅠ

NestedScrollView 안에 있는 RecyclerView는 그 자체 스크롤이 아니라 밖에서 감싸고있는 NestedScrollView 스크롤로 하단에 있는 내용이 보여지고 있는 것 같다. NestedScrollView 작동 방식에 대해서 다시 정리해보겠다.



To Top Button 만들기
=
~~~
** Main.xml **

<android.support.v4.widget.NestedScrollView  
  android:id="@+id/main_scroll"  
  android:layout_width="match_parent"  
  android:layout_height="wrap_content"  
  android:layout_below="@+id/layout_tab"  
>
  <android.support.v7.widget.RecyclerView  
  android:id="@+id/rc_miber"  
  android:layout_width="match_parent"  
  android:layout_height="wrap_content"  
  android:layout_marginTop="@dimen/x27dp">  
  
 </android.support.v7.widget.RecyclerView>
 
</android.support.v4.widget.NestedScrollView>  
  
<ImageButton  
  android:id="@+id/ib_return_top"  
  android:layout_width="@dimen/x62dp"  
  android:layout_height="@dimen/x62dp"  
  android:layout_alignParentBottom="true"  
  android:layout_alignParentRight="true"  
  android:layout_margin="@dimen/x30dp"  
  android:background="@drawable/top_bt"  
  android:visibility="gone"  
  
/>
~~~

~~~
** Main.kt **

override fun onCreate(savedInstanceState: Bundle?) {  
    super.onCreate(savedInstanceState)  
    setContentView(R.layout.activity_miber_list)  
   
   // top button 을 클릭했을 때 top으로 이동하는 부분
   ib_return_top.setOnClickListener{ main_scroll.fullScroll(View.FOCUS_UP) }

	// NestedScrollView 스크롤 listener   
   setListener()
  
}

private fun setListener(){  
  
    main_scroll.setOnScrollChangeListener(NestedScrollView.OnScrollChangeListener { p0, p1, yPosition, p3, p4 ->  
  val visibility =  
            if (yPosition !== 0) View.VISIBLE else View.GONE  
  ib_return_top.visibility = visibility  
    })  
}
~~~


**NestedScrollView 안에 있는 RecyclerView 를 Top으로 스크롤을 올릴 경우 RecyclerView 의 스크롤을 조작하는게 아니라 NestedScrollView의 스크롤을 조작해야한다.** 
(이 경우 RecyclerView의  onScrollChangeListener를 실행시켜도 메소드를 호출하는 순간 한번만 인지하고 그 뒤로 변하는 scroll에 대해서는 인지하지 못한다.)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4Njg2NDMzOV19
-->