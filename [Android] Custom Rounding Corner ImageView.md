ImageView Rounding 문제
=
Glide로 로딩한 이미지가 ImageView에 꽉차게 들어가지 않아 imageView에`android:scaleType="centerCrop"`  설정을 했더니 Glide로 설정했던 corner rounding이 효과가 없어졌다. ImageView에 drawable로 rounding을 줘도 로딩된 이미지가 들어가면 소용이 없었다.

~~~

** RoundishImagView.java **

@SuppressLint("AppCompatCustomView")  
public class RoundishImageView extends ImageView {  
  
    public static final int CORNER_NONE = 0;  
 public static final int CORNER_TOP_LEFT = 1;  
 public static final int CORNER_TOP_RIGHT = 2;  
 public static final int CORNER_BOTTOM_RIGHT = 4;  
 public static final int CORNER_BOTTOM_LEFT = 8;  
 public static final int CORNER_ALL = 15;  
  
 private final RectF cornerRect = new RectF();  
 private final Path path = new Path();  
 private int cornerRadius;  
 private int roundedCorners;  
  
 public RoundishImageView(Context context) {  
        this(context, null);  
  }  
  
    public RoundishImageView(Context context, AttributeSet attrs) {  
        this(context, attrs, 0);  
  }  
  
    public RoundishImageView(Context context, AttributeSet attrs, int defStyleAttr) {  
        super(context, attrs, defStyleAttr);  
  
  TypedArray a = context.obtainStyledAttributes(attrs, R.styleable.RoundishImageView);  
  cornerRadius = a.getDimensionPixelSize(R.styleable.RoundishImageView_cornerRadius, 0);  
  roundedCorners = a.getInt(R.styleable.RoundishImageView_roundedCorners, CORNER_NONE);  
  a.recycle();  
  }  
  
    public void setCornerRadius(int radius) {  
        cornerRadius = radius;  
  setPath();  
  invalidate();  
  }  
  
    public int getRadius() {  
        return cornerRadius;  
  }  
  
    public void setRoundedCorners(int corners) {  
        roundedCorners = corners;  
  setPath();  
  invalidate();  
  }  
  
    public int getRoundedCorners() {  
        return roundedCorners;  
  }  
  
    @Override  
  protected void onSizeChanged(int w, int h, int oldw, int oldh) {  
        super.onSizeChanged(w, h, oldw, oldh);  
  setPath();  
  }  
  
    @Override  
  protected void onDraw(Canvas canvas) {  
        if (!path.isEmpty()) {  
            canvas.clipPath(path);  
  }  
        super.onDraw(canvas);  
  }  
  
    private void setPath() {  
        path.rewind();  
  
 if (cornerRadius >= 1f && roundedCorners != CORNER_NONE) {  
            final int width = getWidth();  
 final int height = getHeight();  
 final float twoRadius = cornerRadius * 2;  
  cornerRect.set(-cornerRadius, -cornerRadius, cornerRadius, cornerRadius);  
  
 if (isRounded(CORNER_TOP_LEFT)) {  
                cornerRect.offsetTo(0f, 0f);  
  path.arcTo(cornerRect, 180f, 90f);  
  } else {  
                path.moveTo(0f, 0f);  
  }  
  
            if (isRounded(CORNER_TOP_RIGHT)) {  
                cornerRect.offsetTo(width - twoRadius, 0f);  
  path.arcTo(cornerRect, 270f, 90f);  
  } else {  
                path.lineTo(width, 0f);  
  }  
  
            if (isRounded(CORNER_BOTTOM_RIGHT)) {  
                cornerRect.offsetTo(width - twoRadius, height - twoRadius);  
  path.arcTo(cornerRect, 0f, 90f);  
  } else {  
                path.lineTo(width, height);  
  }  
  
            if (isRounded(CORNER_BOTTOM_LEFT)) {  
                cornerRect.offsetTo(0f, height - twoRadius);  
  path.arcTo(cornerRect, 90f, 90f);  
  } else {  
                path.lineTo(0f, height);  
  }  
  
            path.close();  
  }  
    }  
  
    private boolean isRounded(int corner) {  
        return (roundedCorners & corner) == corner;  
  }  
}
~~~

~~~

** attrs.xml **
<?xml version="1.0" encoding="utf-8"?>  
<resources>  
	<declare-styleable  name="RoundishImageView"> 
		 <attr  name="cornerRadius"  format="dimension"  />  
		 <attr  name="roundedCorners">  
			 <flag  name="topLeft"  value="1"  />  
			 <flag  name="topRight"  value="2"  /> 
			  <flag  name="bottomRight"  value="4"  />  
			  <flag  name="bottomLeft"  value="8"  />  
			  <flag  name="all"  value="15"  />  
		  </attr>  
	  </declare-styleable>  
  </resources>
~~~

그래서 ImageView를 Custom 해서 사용하는 방법을 선택했다. xml에서는 아래와 같이 사용하면 된다. `app:cornerRadius`로 radius 정도값을 입력 할 수 있고 `app:roundedCorners`로 radius 를 적용할 부분을 설정할 수 있다. 해당 부분의 값은 attrs.xml에서 작성한 값과 같다.

~~~
<com.example.roundcorners.RoundishImageView 
   android:layout_width="match_parent"
   android:layout_height="200dp"  
   android:layout_marginBottom="10dp"  
   android:adjustViewBounds="true"  
   android:scaleType="centerCrop"   
   app:cornerRadius="@dimen/round_corner_radius" 
   app:roundedCorners="topLeft|bottomRight"  />
~~~







출처: https://www.codexpedia.com/android/android-round-corner-imageview/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzODg3NjEyOV19
-->