Content Provider
=
안드로이드 4대 컴포넌트 중 하나인 콘텐트 제공자(Content Provider)는 어플리케이션 내에서 사용할 수 있는 데이터를 '공유'하기 위한 컴포넌트 이며 아래 그림과 같이, `어플리케이션 계층`과 `데이터 계층`을 분리하여 중간 가교 역할을 합니다.
![](https://t1.daumcdn.net/cfile/tistory/22610D3B57E777F032)

어플리케이션은 콘텐츠 제공자에 접근해서 필요한 데이터를 얻어올 수 있습니다. 다양한 데이터를 저장하고 있다가, 어플리케이션의 요청이 들어오면 데이터를 제공한다는 점에서 서버와 비슷한 역할을 한다고 볼 수 있습니다.

Content Resolver
=
폰안에 여러 앱, 여러 프로바이더가 있기 때문에 이들을 관리하고 흐름을 통제한다. 앱이 접근하고자 하는 프로바이더 사이에서 중계자 역할을 합니다.
(query, insert, update, delete)
~~~
ContentResolver  resolver  =  getContentResolver(); 
 Cursor  cursor  =  resolver,  query(DroidTermsExampleContract.CONTENT_URI,  null,  null,  null,  null);
~~~

Content Provider 사용
=
-	manifest에 name, authority 와 등록한다.
-	Uri에 자주 쓰이는 schema, authority, path 등은 String이나 Uri 변수로 설정.
-	앱 내에 사용되는 Uri가 `content://authority` `content://authority/path` 두 가지라면 각각의 경우에 다른 처리가 필요하다. 이를 만약 if문으로 구분하게 되면 경우의 수가 많아지므로 `UriMatcher`를 사용한다

**UriMatcher:**

-	Content Provider가 받는 Uri의 종류를 결정해준다.
-	사용자가 Uri1 / Uri2 를 구분해놓고, 상수 와일드카드(#) 사용할 수 있다.
-	UriMatcher 함수 안에서 NO MATCH 및 추가 MATCH 등록하여 사용하면 편리하다.
~~~
public  static  final  int  CODE_ALL  =  100;
public  static  final  int  CODE_ID  =  101;  
private  static  final  UriMatcher  sUriMatcher  =  buildUriMatcher();  

//아래 함수 작성 후, 프로바이더에서 편하게 사용하기 위해 static 선언 
public  static  UriMatcher  buildUriMatcher()  { 
	UriMatcher  uriMatcher  =  new
	UriMatcher(UriMatcher.NO_MATCH);  uriMatcher.addUri(Contract.AUTHORITY,  Contract.PATH,  CODE_ALL);  
	uriMatcher.addUri(Contract.AUTHORITY,  Contract.PATH  +  "/#",  CODE_ID);  
	// 위 코드는 특정 정수 로우값을 가질 경우 사용  
	return  uriMatcher;  
}
~~~


-	UI에서 데이터를 query(읽기) 할 경우 Resolver를 가져와 query 메소드 호출 (Uri 같이 전달) 
-	Uri의 Authority를 확인하여 매치되는 Provider를 찾아 쿼리 전달 
-	 UriMatcher를 사용해 가져올 데이터 종류 확인 -
-	 Uri와 기타 파라미터를 해독해 알맞은 SQL코드 작성 
-	 해당되는 Data 가져옴 
-	 Cursor 반환


Authority
=
Authority는 특정 콘텐츠 제공자와 상호작용 하는데 사용되기 때문에 이 값은 고유해야 합니다. 그렇기 때문에 도메인 이름과 공급자를 포함하는 패키지의 이름을 함께 선헌하는 것이 좋습니다. 그러면 다른 개발자가 동일한 authority를 가진 content provider를 만들 가능성이 줄어들게 됩니다.

앱 및 기타 앱이 Uri의 형태로 Content Provider를 통해서 데이터를 조작 할 수 있도록 Manifest에 등록합니다.

~~~
content://authority-name/data-in-the-provider
~~~
이것은 http url의 도메인과 유사하게 작동합니다
~~~
http://domain-name/data-in-the-site
~~~



~~~

** Manifest **

<provider  
  android:name="android.support.v4.content.FileProvider" 
  ... 
  android:authorities="kr.co.project.fileprovider"
  ...  
  android:exported="false"  
  android:grantUriPermissions="true"  
  tools:replace="android:authorities">  
 <meta-data  android:name="android.support.FILE_PROVIDER_PATHS"  
  android:resource="@xml/file_path"  
  tools:replace="android:resource"/>  
</provider>


** Activity **

// 갤러리에서 여러 사진을 가져올 수 있는 라이브러리 Matisse 사용
// 사진을 촬영했을 때 저장소 설정 할 때 mani
Matisse.from(this)  
    .choose(MimeType.ofImage())  
    .countable(true)  
    .capture(true)  
    ...
    .captureStrategy(CaptureStrategy(true,"kr.co.project.fileprovider"))  
    ...
    .maxSelectable(10)  
    .restrictOrientation(ActivityInfo.SCREEN_ORIENTATION_UNSPECIFIED)  
    .imageEngine(GlideEngine())  
    .forResult(PHOTO_REQUEST_CODE)
    
~~~

갤러리에서 여러장의 사진을 가져올 수 있는 라이브러리 Matisse 를 사용한 경우를 예시로 들면, 사진을 촬영했을 때 저장할 저장소를 설정할 때 Manifest에 등록한 authority와 CaptureStrategy의 두번째 인자인 authority가 `kr.co.project.fileprovider`로 같은 것을 볼 수 있습니다.
**Manifest에 등록한 authority와 app에서 사용하는 authority가 같아야 제대로 동작합니다**


----
참고: https://bitsoul.tistory.com/155
https://blog.yena.io/studynote/2017/11/11/Android-Content-Provider.html
https://stackoverflow.com/questions/24189678/android-content-provider-authorities
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNjk0MDQ5NjZdfQ==
-->