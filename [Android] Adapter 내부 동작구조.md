Adapter
=


Adapter는  **onCreateViewHolder, onBindViewHolder ,getItemCount ,getItemViewType** 이 4개의 메소드를 통해서 data를 binding한다.

-  **getItemCount :** 총 item 갯수가 몇개 인지 판단
- **getItemViewType :** 현재 item view의 position에 해당하는 viewType을 판단
- **onCreateViewHolder :** viewType에 해당하는 ViewHolder를 생성하여 return (ViewHolder에서 각 item view의 정보를 갖고있다. Adapter는 계속해서 ViewHolder를 이용해 item view를 관리할 것)
- **onBindViewHolder :** 생성된 viewHolder와 position을 전달받아서,현재 position에 맞는 data를 viewHolder가 관리하는 view들에 binding 

폰 화면에 10개의 list가 보인다면, 맨처음 getItemCount가 불리고, 그 후 10번 getItemViewType, onCreateViewHolder, onBindViewHolder가 연속적으로 호출 될 것이다.

  
  
### Adapter 내부동작
간단히 보면 이렇고  내부적으로 어떻게 동작하는지를 살펴보면 view의 layout pass에서, LayoutManager의 onLayoutChildren가 호출되고 이 메소드 내에서 타고타고 가다보면, Recycler 내의 **getViewForPosition**이라는 메소드가 호출되는데 이 부분에서 Adapter의 4개의 메소드가 설명한 순서대로 불리게 된다.

RecyclerView의 꽃인 view 재사용에 대해서 설명하면서, 더 자세히 알아보자. 화면의 스크롤을 내려서 11번, 12번, 13번의 item view가 보이게 된다면 내부적으로 어떤 동작이 이루어질까? 여기서 **scrapped view**라는 개념이 사용된다.

scrapped view란, 아직 RecyclerView에는 붙어있지만, 곧 제거되거나 재사용될 것으로 지정된 viewHolder이다. RecyclerView내의 Recycler라는 class는 **scrapped view들의 pool을 관리하는 RecycledViewPool class를 이용하여 scrapped view를 관리한다.**

 LayoutManager가 item view들을 언제 재사용할지에 대한 정책을 결정한다.

즉, LayoutManager가 어떤 viewholder를 scrapped view로 지정할 것인지에 대해 책임을 지고 Recycler는 LayoutManager에서 scrapped view로 지정한 viewholder들을 RecycledViewPool을 통해서 관리한다고 생각하면 되겠다.

  

![](http://postfiles8.naver.net/20160413_295/mail1001_1460535517642jTwnI_PNG/3.png?type=w2)

  

스크롤을 아래로 내리면, LinearLayoutManger의 scrollVerticallyBy 메소드가 호출되고 이 메소드 내에서 타고타고 가다보면, 어떤 viewholder를 scrapped view로 지정할 것인지에 대해서 결정하고 (스크롤을 아래로 내리면, 맨 위에 애들부터 scrapped view로 지정된다.) 그 후 위에서 언급했던 Recycler 내의 getViewForPosition이라는 메소드가 호출된다.

Recycler의 getViewForPosition 메소드는 현재 LayoutManager가 배치하고자 하는 view의 position을 전달인자로 받아서, 이 position에 맞는 view를 반환하는 메소드이다.

Recycler는 position에 알맞는 view를 판단하기 위해서 일단 adapter의 getItemCount를 통해서 아이템 수를 얻어와 유효한 position인지 체크하고, getItemViewType을 호출해서 현재 position의 viewType을 알아낸다.

  
그리고, onCreateViewHolder를 하기전에 scrapped view pool에 현재 viewType과 같은 ViewHolder가 있다면 그 ViewHolder를 얻어오고 create하지 않는다.
이게 바로, RecyclerView가 공간을 재사용하는 방법이다!!
기존에 생성되어있던 ViewHolder 중 더 이상 사용되지 않는 ViewHolder를 가지고 와서 쓰는 것이다.

이제 마지막으로 onBindViewHolder를 호출하여 viewHolder를 인자로 넘겨주어 viewHolder내의 view들에 data를 binding한다.

----
**[출처]**  [Android RecyclerView에 대하여 - View가 재사용되는 내부동작에 대한 고찰](http://blog.naver.com/mail1001/220682221473)|**작성자**  [초코라떼](http://blog.naver.com/mail1001)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk4MjY3NzY3OV19
-->