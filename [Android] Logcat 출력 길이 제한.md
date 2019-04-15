로그캣은 한번에 출력할 수 있는 출력 길이 제한이 있다. 이 값은 단말에 따라 제한을 받는 것으로, 아래와 같은 명령어를 통해 확인할 수 있다.
~~~
>adb  logcat -g

main: ring buffer is 2MB (1MB consumed), max entry is 5120b, max payload is 4076b
system: ring buffer is 256Kb (255Kb consumed), max entry is 5120b,  max payload is 4076b
~~~
이 값 중에서 max entry와 max payload 부분에 영향을 받는다. 이 값은 커널에 하드코딩되어 있어 어플리케이션 개발자가 수정이 불가능하다.

~~~
#define LOGGER_ENTRY_MAX_LEN (4*1024)
#define LOGGER_ENTRY_MAX_PAYLOAD \ (LOGGER_ENTRY_MAX_LEN - sizeof(struct logger_entry))
~~~
로그가 짤리지 않고 모두 출력되길 바란다면, 로그를 적당히 잘라서 보여주는 방법이 가장 일반적이다.

~~~
String  msg  =  "your log message.";
while( msg.length() > 0 ){

	if( msg.length() > 4000 ){
		Log.i( _tag, msg.substring( 0, 4000 ));
		msg = msg.substring( 4000 );
	}else{
		Log.i(  _tag,  msg  );
	}
}
~~~

위와 같은 방법으로 로그를 나눠서 보여줄 수 있다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyMjY2NzkxN119
-->