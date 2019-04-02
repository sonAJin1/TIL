
text color 바꾸기
~~~
private fun setTabTextColor(){  
    binding.tabs.setSelectedTabIndicatorColor(Color.parseColor("#4D333333"))  
    binding.tabs.setTabTextColors(Color.parseColor("#4D333333"),Color.BLACK)  
}
~~~

--------

tab under bar color 바꾸기
~~~
<android.support.design.widget.TabLayout  
  ....
  ....
  .... 
  app:tabIndicatorColor="@color/black"  
>
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ4NjIzOTA3OF19
-->