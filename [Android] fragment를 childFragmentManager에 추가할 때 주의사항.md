Fragment를 childFragmentManager에 추가할 때 주의사항
=

fragment를 childFragmentManager에 추가할 때 add 말고 replace로 추가하자. 안그러면 새로고침할 때 fragment가 쌓이는 문제가 발생한다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTM1MzMwNDEzXX0=
-->