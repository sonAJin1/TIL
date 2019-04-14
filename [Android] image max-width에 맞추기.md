`android:adjustViewBounds="true"`

~~~
<ImageView  
  android:id="@+id/iv_image"  
  android:layout_width="match_parent"  
  android:layout_height="wrap_content"  
  android:scaleType="fitXY"  
  android:adjustViewBounds="true"  
/>

Glide.with(context)  
    .load(url)  
    .fitCenter()  
    .placeholder(R.drawable.icon_noimage_1)  
    .error(R.drawable.icon_noimage_1)  
    .into(imageView)
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTczNjMzODM4N119
-->