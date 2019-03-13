Rounding corner 그라디언트 적용
=

~~~

private fun setGradientBackground(){

	var topColor = 0  
	var bottomColor = 0 
 
	when(item.theme){ 
	  "THEME01"-> {  
	        topColor = 	ContextCompat.getColor(context,R.color.theme01_background_top)  
	        bottomColor = ContextCompat.getColor(context,R.color.theme01_background_bottom)  
	    }  
	    "THEME02"-> {  
	        topColor = ContextCompat.getColor(context,R.color.theme02_background_top)  
	        bottomColor = ContextCompat.getColor(context,R.color.theme02_background_bottom)  
	    }  
	}  
  
	var rd  = GradientDrawable(GradientDrawable.Orientation.TOP_BOTTOM,  
  intArrayOf(topColor, bottomColor))  
	rd.cornerRadius = convertDPToPixels(8f,context)  
	binding.llBackground.background = rd

}

private fun convertDPToPixels(dp: Float, context: Context): Float {  
    return TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_DIP, dp, context.resources.displayMetrics)  
  
}


~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYyMTk5Njc4OSw3MzA5OTgxMTZdfQ==
-->