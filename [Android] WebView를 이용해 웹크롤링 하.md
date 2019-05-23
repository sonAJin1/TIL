
Android에서 WebView를 이용해 웹크롤링 하기
=

웹 크롤링을 하다보면 단순히 request를 보내고, 해당 response 값을 해석하는 것만으로는 부족한 경우가 있다. 수집 목적에 따라 해당 **웹 페이지에서 반드시 자바스크립트가 실행된 이후의 결과를 추출해야 할 때도 있고, 아예 자신이 정의한 자바스크립트를 실행시켜야 할 수도 있다.**


WebView 사용하기
=

**1. WebView 타겟 사이트를 로드.(실제 웹 브라우저와 다름없기 때문에 JS도 다 실행됨)**

**2. 해당 WebView에서 자바스크립트를 실행하여 어플리케이션 쪽으로 html 소스 전송**

**3. JavascriptInterface를 사용하여 전송받은 html 소스 받기**

**4. Jsoup로 파싱하여 크롤링.**

---


간단한 예시를 만들어 보자. 
~~~
class MainActivity : AppCompatActivity() {  
  
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        setContentView(R.layout.activity_main)  
  
        webView.settings.javaScriptEnabled = true  
  
		webView.addJavascriptInterface(MyJavascriptInterface(), "Android")  
  
        webView.webViewClient = object : WebViewClient() {  
            override fun onPageFinished(view: WebView?, url: String?) {  
                super.onPageFinished(view, url)  
  
                view!!.loadUrl("javascript:window.Android.getHtml(document.getElementsByTagName('body')[0].innerHTML);")  
  
  
            }  
        }  
  
  
        //지정한 URL을 웹 뷰로 접근하기  
		webView.loadUrl("https://www.naver.com")  
  
  
    }  
  
    class MyJavascriptInterface {  
        @JavascriptInterface  
		 fun getHtml(html: String) {  
            //위 자바스크립트가 호출되면 여기로 html이 반환됨  
			var source = html  
            Log.e("html: ",source)  
  
            val doc = Jsoup.parse(source)  
  
            val title = doc.select("tit")  
            Log.d("result: ", "doc= $doc")  
            Log.d("result: ", "title= $title")  
        }  
  
    }  
}
~~~

**주의사항**

WebView의 `visibility`를 Gone이나 invisible로 설정해두면 html 값을 가져오지 못한다

----
**[참고]** 
[[Android] WebView를 이용해 웹 크롤링하기](https://blog.naver.com/shino1025/221451362161)|**작성자** [IML](https://blog.naver.com/shino1025)
[https://softwarelogy.com/html-parse-in-kotlin-with-jsoup/](https://softwarelogy.com/html-parse-in-kotlin-with-jsoup/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzIwNzk2MzNdfQ==
-->