Retrofit2 POST @Field Parameters encoding 오류
=

~~~
@POST("/users/join")  
fun login(  
    @Field("name") name:String,  
	@Field("email") email:String,  
	@Field("company") company:String,  
) : Call<JSONObject>
~~~
이런식으로 @POST에 @Field로 파라미터를 더해서 보내게 되면 `java.lang.IllegalArgumentException: @Field parameters can only be used with form encoding. (parameter #1)` 라는 오류가 나게 된다.

아래와 같이 **@FormUrlEncoded** 어노테이션을 붙여줘야 `form-encode 형식`으로 파라미터가 정상적으로 전송된다.

~~~
@FormUrlEncoded  
@POST("/users/join")  
fun login(  
    @Field("name") name:String,  
 @Field("email") email:String,  
 @Field("company") company:String,  
 @Field("imei") imei:String  
) : Call<JSONObject>
~~~
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTczNTU2MDQzMF19
-->