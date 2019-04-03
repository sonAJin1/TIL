
Android kotlin SingleChoiceItem Dialog 선택 값 가져오기
=
~~~
private fun selectCategoryDialog(){  
    val items = arrayOf("상품문의", "취소환불문의", "결제문의", "서비스문의", "계정문의","기타")  
    var selectCategory = ""  
  var builder = AlertDialog.Builder(this)  
    builder.setTitle("문의 카테고리 선택")  
    builder.setSingleChoiceItems(items,-1) {  
  dialog, which ->  
  selectCategory = items[which]  
  
    }  
  .setPositiveButton("ok") { dialog, which ->  
   // 여기서 SelectCategory 값을 받아서 처리할 수 있음
        }  
  .setNegativeButton("cancel") { dialog, which -> }  
  builder.create().show()  
}
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxMDg4MDcwMF19
-->