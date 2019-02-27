

<h1 id="bindingadapter-파라미터-2개일-때">BindingAdapter 파라미터 2개일 때</h1>
<p>BindingAdapter를 사용할 때 파라미터를 2개 이상 사용하고 싶은 경우가 있습니다.</p>
<p>아래의 경우는 파라미터 하나만 사용하는 경우의 예시 입니다</p>
<pre><code>@JvmStatic  
@BindingAdapter("imageResource")  
fun setImageResource(imageView: ImageView, resource: Int) {  
  
    Glide.with(imageView.context)  
            .load(resource)  
            .asBitmap()  
            .placeholder(R.drawable.icon_noimage_1)  
            .format(DecodeFormat.PREFER_ARGB_8888)  
            .into(object : SimpleTarget&lt;Bitmap&gt;() {  
  
                override fun onResourceReady(resource: Bitmap, glideAnimation: GlideAnimation&lt;in Bitmap&gt;) {  
                    imageView.setImageBitmap(resource)  
  
                }  
            })  
}
</code></pre>
<pre><code>&lt;ImageView  
  android:id="@+id/iv_image"  
  android:layout_width="@dimen/x20dp"  
  android:layout_height="@dimen/x20dp"  
  app:imageResource="@{data.img}"/&gt;
</code></pre>
<h4 id="파라미터가-한-개-이상일-경우-하나당-xml-속성이-추가됩니다">파라미터가 한 개 이상일 경우 하나당 xml 속성이 추가됩니다</h4>
<pre><code> @JvmStatic  
 @BindingAdapter("imageResource", "noImage")  
    fun setImageResource(imageView: ImageView, url: String, noImage: Drawable) {  
        if (TextUtils.isEmpty(url)) {  
            imageView.setImageDrawable(placeHolder)  
        } else {  
            Glide.with(imageView.context)  
                    .load(url.trim { it &lt;= ' ' })  
                    .crossFade()  
                    .placeholder(noImage)  
                    .error(noImage)  
                    .bitmapTransform(CropCircleTransformation(imageView.context))  
                    .into(imageView)  
        }  
    }  
}
</code></pre>
<pre><code>&lt;ImageView  
  android:id="@+id/iv_image"  
  android:layout_width="@dimen/x20dp"  
  android:layout_height="@dimen/x20dp"  
  app:imageResource="@{data.img}"
  app:noImage="@{@drawable/no_image}"
  /&gt;
</code></pre>

