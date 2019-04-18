키보드 검색 버튼 생성 후 Listener
=
~~~
** XML **

<EditText android:imeOptions="actionSearch"/>

~~~


~~~

** kotlin **

private fun setSearchListener(){  
    editText.setOnEditorActionListener(object : TextView.OnEditorActionListener {  
        override fun onEditorAction(v: TextView?, actionId: Int, event: KeyEvent?): Boolean {  
            if (actionId == EditorInfo.IME_ACTION_SEARCH) {  
                search()  
                return true  
			}  
            return false  
		}  
    })  
}

~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MDAwMTY0MTFdfQ==
-->