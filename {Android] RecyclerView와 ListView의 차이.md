RecyclerView와 ListView차이
=

### ListView :

    @Override  
	public View getView(final int position, View convertView, ViewGroup parent) {  
	 Holder holder = new Holder();  
	 View rowView = inflater.inflate(R.layout.item_list, null);  
	 holder.tv = (TextView) rowView.findViewById(R.id.text);  
	 holder.img = (ImageView) rowView.findViewById(R.id.image);  
	 holder.tv.setText(result[position]);  
	 holder.img.setImageResource(imageId[position]);  
	 rowView.setOnClickListener(new OnClickListener() {  
	 @Override  
	 public void onClick(View v) {  
	 // TODO Auto-generated method stub  
	 Toast.makeText(context, "You Clicked " + result[position], Toast.LENGTH_LONG).show();  
	 }  
	 });  
	 return rowView;  
	}

가장 일반적인 ListView의 getView() 접근 방식이다. 하지만 위와 같이 동작하게 되면 getView()는 현재 화면상에 아이템이 보일 때 호출되는 함수이기 때문에 아이템이 20개가 있고 이를 스크롤한다고 가정하면 스크롤 시에도 getView() 함수는 계속해서 호출이 되면서 **재사용성이 떨어지게 된다.**

또한, 별도의 null 처리가 없으므로 스크롤 할 때마다 inflate를 통해서 View의 create가 발생하고 findViewById도 함께 호출된다. 
리스트 특성상 하나의 view가 연속적으로 사용이 가능한 형태가 만들어지면 되는데 ListView는 이러한 것이 강제적이지 않다.

그래서 `ViewHolder`라는 개념이 등장하게된다. 

**ViewHolder** 는 UI를 수정할 때 마다 부르는 findViewById()를 ViewHolder 패턴을 이용해 한번만 호출되게 하므로서 리스트 뷰의 지연을 초래하는 무거운 연산을 줄여준다. 
ViewHolder 패턴은 ListView의 재사용성의 문제를 줄여주었기 때문에 ViewHoler 패턴이 적용된 ListView와 RecyclerView의 성능상의 차이는 미세하다.

### RecyclerView :

롤리팝(5.0) 버전이 ListView보다 유연하고 성능이 향상된 RecyclerView와 함께 발표되었다. 기존의 ListView는 커스터마이징 하기에 힘들었고, 구조적인 문제로 성능상의 문제도 있었기 때문이다.

RecyclerView는 ListView의 문제를 해결하기 위해 개발자에게 더 다양한 형태로 커스터마이징 할 수 있도록 제공되었다. RecyclerView와 ListView의 가장 큰 차이점은 **LayoutManager와 ViewHolder 패턴의 의무적인 사용, Item에 대한 뷰의 변형이나 애니메이션할 수 있는 개념이 추가되었다.**

![creating Lists and cards](https://woovictory.github.io/img/android_recyclerview.png)

widget인 RecyclerView는 LayoutManager를 통해서 View를 그리는 방법을 정의한다. RecyclerView.Adapter에서는 Data의 ViewHolder 정의에 따라서 UI가 선택되고 이를 표현하게 된다.

**RecyclerView 장점 :**

- 강제적인 ViewHolder의 적용으로 View의 재사용을 가능하게해줌
- RecyclerView.ItemAnimator을 이용하여 Item의 Animator를 이용할 수 있다.
- LayoutManager를 통해서 아이템의 배치 방법을 다양하게 적용할 수 있다.

### RecyclerView 주요 클래스 :

**Adapter :**
	리스트뷰는 데이터가 어디서 왔느냐에 따라 BaseAdapter를 상속한 ArrayAdapter(배열로부터 데이터를 가져올때 사용), CursorAdapter(DB로 부터 데이터를 가져올 때 사용), SimpleAdapter(XML 등으로부터 가져올 때 사용)을 구분하여 사용한다.

하지만 RecyclerView는 모든 상황에 사용할 수 있는 Adapter를 사용하여 데이터를 처리하여 ListView의  Adapter보다 **유연성**이 뛰어난 것을 볼 수 있다.

RecyclerView의 Adapter는 다음의 3가지 인터페이스를 구현해야한다.

- onCreateViewHolder : 뷰홀더를 생성하고 뷰를 붙여주는 부분이다.
- onBindViewHolder : 재활용되는 뷰가 호출하여 실행되는 메소드, 뷰 홀더를 전달하고 어댑터를 position 의 데이터를 결합시킨다.
- getItemCount() : 데이터의 개수 반환

getItemCount() -> onCreateViewHolder() -> onBindViewHolder() 순으로 호출된다.

ListView가 사용했던 getView() 메소드는 매번 호출되면서 null 처리를 해주는 귀찮은 작업을 해줘야했다면,  onCreateViewHolder는 새롭게 생성될 때만 호출된다.

**ViewHolder :**
ListView에서는  ViewHolder 패턴을 권장했다. RecyclerView에서는 ViewHolder 패턴을 강제하는 방법으로 재사용 문제가 일어나는 것을 방지했다.

**LayoutManager :**
ListView는 수직 스크롤만 가능하다. 수평으로는 사용할 수 없었다. 그러나 이제 RecyclerView에서는 수직뿐만 아니라 수평 스크롤 또한 지원한다. 뿐만 아니라 더 다양한 타입의 리스트들을 지원하고, 커스텀할 수 있도록 해준다.


### 정리

![enter image description here](https://woovictory.github.io/img/android_diff_listview_recyclerview.png)



-----
참고 : [https://woovictory.github.io/2019/01/03/Android-Diff-of-ListView-and-RecyclerView/](https://woovictory.github.io/2019/01/03/Android-Diff-of-ListView-and-RecyclerView/)
[https://crystal-k.tistory.com/16](https://crystal-k.tistory.com/16)
[https://armful-log.tistory.com/27](https://armful-log.tistory.com/27)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjMzNTYzMDE2XX0=
-->