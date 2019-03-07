Marshalling
=
마샬링은 데이터를 바이트 덩어리로 만들어 스트림에 보낼 수 있는 형태로 바꾸는 변환 작업을 뜻합니다. 자바에서 마샬링을 적용할 수 있는 데이터는 원시 자료형 (boolean, char, byte, short, int, long, float, double)와 객체 중에서 Serializable 인터페이스를 구현한 클래스로 만들어진 객체입니다. 객체 원시 자료형과 달리 일정한 크기를 가지지 않고 객체 내부의 멤버 변수가 다르기 때문에 크기가 천차만별로 달라집니다. 이런 문제점을 처리할 수 있는게 ObjectOutputStream 클래스입니다.

Unmarshalling
=
언마샬링은 객체 스트림을 통해서 전달된 바이트 덩어리를 원래의 객체로 복구하는 작업입니다. 이 작업을 제대로 수행하기 위해서는 반드시 어떤 객체 형태로 복구할지 형 변환을 정확하게 해줘야 제대로 실행됩니다.


객체 직렬화 ObjectInputStream / ObjectOutputStream
=
마샬링과 언마샬링은 자바에서 객체 안에 있는 내용을 파일로 저장하거나 네트워크로 전송하는 작업에 사용됩니다. 이를 위해서는 객체를 바이트 형태로 분해해야하기 때문입니다. ObjectInputStream과 ObjectOutputStream은 이를 위하여 객체를 직접 입출력 할 수 있도록 해주는 객체 스트림입니다.

- **객체 전송의 단계**
	객체를 분해하여 전송하기 위해서는 직렬화(Serialization) 되어야 합니다.
	객체를 전송하기 위해서는 3단계를 거칩니다.
	1. 직렬화된 객체를 바이트 단위로 분해한다 (marshalling)
	2. 직렬화 되어 분해된 데이터를 순서에 따라 전송한다.
	3. 전송받은 데이터를 원래대로 복구한다 (unmarshalling)
	
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzEwMDE3OTNdfQ==
-->