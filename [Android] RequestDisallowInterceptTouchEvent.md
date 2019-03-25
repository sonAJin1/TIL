RequestDisallowInterceptTouchEvent
=
RequestDisallowInterceptTouchEvent는 Scrollview 안에 또 다른 스크롤 기능이 들어가는 View를 사용할 때 사용하여, 부모에게 Touch Event를 빼앗기지 않을 수 있게 하는 기능이다.

~~~

** ParentViewFragment **

fun getSwipeView(): SwipeRefreshLayout{  
     return binding.swipeRefreshLayout  
}

~~~

~~~

** ChildViewFragment **

override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
 
 val parentFrag = this.parentFragment as FeedMainFragment 
 val parentSwipe = parentFrag.getSwipeView()
 setParentScrollTouchListener(parentSwipe)
 }


@SuppressLint("ClickableViewAccessibility")  
private fun setParentScrollTouchListener(parentScroll: ScrollView){  
    binding.rcList.setOnTouchListener(object : View.OnTouchListener {  
        override fun onTouch(v: View?, event: MotionEvent?): Boolean {  
            var action = event?.action  
  when(action){  
                MotionEvent.ACTION_DOWN->{parentScroll.requestDisallowInterceptTouchEvent(true)}  
                MotionEvent.ACTION_UP->{parentScroll.requestDisallowInterceptTouchEvent(true)}  
                MotionEvent.ACTION_SCROLL->{parentScroll.requestDisallowInterceptTouchEvent(true)}  
  
            }  
            return false  
  }  
  
    })  
}
~~~


ParentViewFragment 에서 부모 scroll을 가져와서 childView에서 스크롤 되는 뷰가 MotionEvent를 할 때 requestDisallowInterceptTouchEvent 값을 true로 바꿔서 움직임을 제한한다

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM5MDgyMzUxXX0=
-->