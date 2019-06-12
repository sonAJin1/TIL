RTSP 단점
=
라이브 스트리밍을 위한 전통적인 프로토콜인 RTSP는 `도입 비용이 높고` `방화벽 환경에서 서비스가 원활하게 이루어지지 않는다`는 단점이 있다. 이러한 단점을 해결하는 방법으로 HTTP를 라이브 스트리밍을 위한 프로토콜로 사용하는 방법이 나오게 되었다. HTTP를 이용해 원활한 스트리밍 서비스를 제공하려는 방법 중 Apple이 만든  HLS에 대해 살펴보자.

 Live Streaming
=
라이브 스트리밍에서는 비디오와 오디오를 실시간으로 인코딩해 많은 사용자에게 동시에 보낼 수 있어야한다. 라이브 스트리밍을 위한 전통적인 프로토콜로는 RTSP(Real-Time Streaming Protocol)/RTP(Real-time Transport Protocol), RTMP(Real-Time Messaging Protocol) 등이 있다. 이 프로토콜을 사용하는 스트리밍 서버는 영상 데이터의 전송뿐만 아니라, **동영상에 대한 정보 분석이나 전송 규격에 맞도록 동영상 파일을 읽어서 변형하는 기능도 갖춰야 한다.** 고가의 도입 비용 이외에도 결정적인 단점이 있다. 현재 가장 많이 사용하는 RTSP/RTP의 경우, 서로 다른 네트워크 연결을 통해 데이터를 교환하기 때문에 방화벽이나 NAT(Network Address Translator)를 많이 쓰고 있는 환경에서는 서비스가 원활하지 않은 문제가 있다. 그래서 대안으로 나온 것이 HTTP를 전송 채널로 사용하는 것이다. HTTP는 양방 방식이 아니기 때문에 라이브 스트리밍을 위해서는 단점을 극복할 별도의 방식이 필요하지만, **방화벽에서 HTTP 서버로의 요청만 통과시키면 되기 때문에 방화벽의 설정이 단순해진다. 요청과 응답이 1:1로 대응되기 때문에 NAT 환경에서도 서버와 통신하는 것이 쉽다.** 이러한 장점 이외에도, 웹서비스를 위한 캐시 구조를 그대로 사용할 수 있고, 기존에 구축되어 있는 CDN(Content Delivery Network)도 특별히 변경하지 않고 그대로 이용할 수 있다는 것이 장점이다




----
출처 : [https://idlecomputer.tistory.com/93?category=772007](https://idlecomputer.tistory.com/93?category=772007)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MDczMDU0MzhdfQ==
-->