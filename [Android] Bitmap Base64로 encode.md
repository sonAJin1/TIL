
**BitmapEncoding**
~~~
private fun encodeImageFileToBase64(bitmap:Bitmap):String{  
    val immagex = bitmap  
    val baos = ByteArrayOutputStream()  
    immagex.compress(Bitmap.CompressFormat.JPEG, 100, baos)  
    var byte = baos.toByteArray()  
    var imageEncoded = Base64.encodeToString(byte,Base64.DEFAULT)  
    XLog.e("encodeFile: $imageEncoded")  
    return imageEncoded  
}
~~~

**사진 받아오는 곳**
~~~
 override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {  
        super.onActivityResult(requestCode, resultCode, data)  
  if(resultCode== Activity.RESULT_OK && requestCode == PHOTO_REQUEST_CODE){  
  
            var imageStream : InputStream? = null  
  
 var photoList : List<Uri> = Matisse.obtainResult(data)  
            for(photo in photoList){  
               addPhoto(photo.toString())  
                try{  
                    imageStream = applicationContext.contentResolver.openInputStream(photo)  
                }catch (e: Exception){  
                    e.message }  
  
                var bitmapPhoto = BitmapFactory.decodeStream(imageStream)  
                encodeImageFileToBase64(bitmapPhoto)  
            } 
        }  
    } // onActivityResult end ------
~~~

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY5MzQyODYyNV19
-->