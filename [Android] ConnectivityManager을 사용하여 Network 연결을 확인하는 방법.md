ConnectivityManager을 사용하여 Android Network 연결 확인하는 방법
=

Splash 화면에서 네트워크가 연결이 되어 있는지 확인을 해주는데, 로그인 기능이 없는 경우 Splash 화면에서 자동로그인을 확인하는 등 서버와 통신할 경우가 없기때문에 Android의 `ConnectivityManager`를 사용하여 네트워크 연결을 확인하는 방법을 사용해서 구현해보자.

먼저 네트워크 연결을 확인하는 ConnectivityHelper 클래스를 만든다.
~~~
object ConnectivityHelper {  
    fun isConnectedToNetwork(context: Context): Boolean {  
        val connectivityManager = context.getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager  
  
        var isConnected = false  
 if (connectivityManager != null) {  
            val activeNetwork = connectivityManager.activeNetworkInfo  
  isConnected = activeNetwork != null && activeNetwork.isConnectedOrConnecting  
  }  
  
        return isConnected  
    }  
}
~~~

방금 만든 ConnectivityHelper를 SplashActivity에서 호출하여 네트워크가 연결되어있을 때, 안되어있을 때 구분하여 동작을 구현한다.
~~~
class SplashActivity : AppCompatActivity() {  
  
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        setContentView(R.layout.activity_splash)  
  
  
        if (ConnectivityHelper.isConnectedToNetwork(this)) {  
			  Log.e("network: ","connect")  
        } else {    
			  Log.e("network: ","disconnect")  
        }  
    }  
}
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1NTc0NTg4Ml19
-->