~~~
val builder = AlertDialog.Builder(ContextThemeWrapper(``this``@SplashActivity``, R.style.Theme_AppCompat_Light_Dialog))
	builder.setTitle("제목(kotlin)")
	builder.setMessage("내용(Kotlin)")
	builder.setPositiveButton("확인") { _, _ ->
	Log.e("alert ok")
}

builder.setNegativeButton(``"취소"``) { _, _ ->

(``"alert cancel"``)

`}`

`builder.show()`
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1ODAzNDUyNjFdfQ==
-->