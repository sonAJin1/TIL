
~~~
private fun getRealPathFromURI(uri:Uri):String{  
  
  
    var result =uri.toString()  
    var cursor = contentResolver.query(uri,null,null,null,null)  
  
    try {  
        if(cursor!=null){  
            cursor.moveToFirst()  
            var idx = cursor.getColumnIndex(MediaStore.Images.ImageColumns.DATA)  
            result = cursor.getString(idx)  
            cursor.close()  
        }  
        return result  
    }catch (e: Exception){  
  
    }  
  
    Log.e("result: $result")  
    return result  
}
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MTkwNTkzMjVdfQ==
-->