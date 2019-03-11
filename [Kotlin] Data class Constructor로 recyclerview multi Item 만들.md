Constructor
=
Kotlin에서 recyclerView Model 로 사용하는 data class를 사용하다가 여러 ViewType에 맞춰 Model 의 내용이 달라져야 하는 상황이 있었습니다

~~~
  
class RecyclerViewAdapter(private val context: Context) :  RecyclerArrayAdapter<Any, ItemListAdapter.SetViewHolder>() {  

 override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): SetViewHolder {  
        val binding = DataBindingUtil.inflate<ViewDataBinding>(LayoutInflater.from(parent.context), R.layout.item_curation, parent, false)  
  
        return SetViewHolder(binding)  
    }  
  
    override fun onBindViewHolder(holder: SetViewHolder, position: Int) {  
  
        val item = getItem(position)!!  
        val binding = holder.binding  
  
  
    fun setListener(listener: ItemListAdapter.OnClickListener) {  
        this.listener = listener  
    }  
  
    interface OnClickListener {  
        fun onSelectItem(item : Any)  
    }  
  
    class SetViewHolder(itemBinding: ViewDataBinding) : RecyclerView.ViewHolder(itemBinding.root)  {  
        val binding: ItemCurationBinding = itemBinding as ItemCurationBinding  
    }  
  
}
~~~

이런 구조로 사용하고 있어서 Item list 를 추가하기 번거로운 상황이었기 때문에 data class 로 만들어 둔 Model 부분을 constructor 로 생성자를 만들어 데이터를 유연하게 받을 수 있도록 변경하는 방법을 사용해봤습니다.


~~~
data class Item (var id:String,var name:String, var summary:String?=null){  
  constructor(id:String, name:String) : this(id,name,null)
~~~

경우에 따라 null로 받고싶은 부분은 **String?=null** 을 이용하여 선언하고 this 로 상속 받을 때 null 처리를 해서 사용합니다.  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2MTgyMTcxXX0=
-->