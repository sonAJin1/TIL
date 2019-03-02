
Kotlin의 기본 for문 형식
=
Kotlin에서의 for문은 java와는 다르게 초기식; 조건식; 증감식; 의 구성형태를 지원하지 않고
java의 each-for문의 형태를 가집니다

  Kotlin에서 for문의 형식은
```
for (반복 대상 요소 저장변수 in 반복 대상)  
```
으로 이루어져 있습니다


- in 왼쪽에는 오른쪽의 배열요소의 값이 반복 저장될 변수(item)이 오고, 오른쪽에는 반복대상(배열, 컬랙션)이 위치합니다

- 저장소 타입은 배열 또는 컬랙션에 저장된 원소의 타입과 동일하게 설정됩니다



 
 Kotlin으로 3가지 구성형태의 for문
 =
 java의 기존의 (int i=0; i<10; i++) 형태를 띄는 for문은 **while문으로 대체하거나 range를 사용하여 구현할 수 있습니다**

  

Range는 ".." operator 를 갖는 rangeTo 함수로 표현합니다.

아래의 예시는 JAVA 언어의 if (int i=1; i<30; i++) 조건문과 같은 의미를 가집니다.

단 점점 커지는 수가 아니라 작아지는 수라면 아무것도 수행하지 않게 됩니다.

```
 for (i in 1..10) //prints "1부터 10"
 for (i in 10..1) // prints nothing
```

java에서 for (int i = 4 ; i > 0 ; i --) 와 같이 사용되는 반복문을Kotlin에서는 downTo() 함수를 통해 아래와 같이 표현할 수 있습니다.

```
for (i in 10 downTo 1)  // prints "10부터 1"
```

또한 step을 사용하여 일정한 간격으로 i를 증가시킬 수도 있고,

DownTo와 step을 함께 사용하여 역순으로 일정간격으로 i를 감소시킬 수도 있습니다.

```
for (i in 1..4 step 2) print(i) // prints "1,3"

for (i in 4 downTo 1 step 2) print(i) // prints "4,2"
```

until 함수를 사용하여 범위를 결정할 수도 있습니다.

(아래의 식에서 i는 1에서 9까지만 수행합니다. 10은 포함되지 않습니다.)

```
for (i in 1 until 10) { // i in [1, 10), 10 is excluded
     println(i)
}
```

last 함수를 사용하여 마지막 i 값을 확인할 수 있습니다.

```
(1..12 step 2).last == 11  // progression with values [1, 3, 5, 7, 9, 11]
(1..12 step 3).last == 10  // progression with values [1, 4, 7, 10]
(1..12 step 4).last == 9   // progression with values [1, 5, 9]
```

  

  

  

출처 : https://codetravel.tistory.com/24

https://codedragon.tistory.com/4425
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY5OTAzNzQzMywxNzA1NTA1MDYsMTgyOT
M2NTk3OV19
-->