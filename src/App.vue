<template>
<!-- header -->
<NavPrice :cart="cart"/>
<!-- box 상품선택 -->
  <div id="box">
    <ul class="form">
      <li>
        <span>
          <label for="userMax">최고값</label>
          <input id="userMax" v-model="max" readonly />
        </span>
        <span>
         선택상품 갯수: {{filteredProducts.length}}
        </span>
      </li>
      <li>
        <input type="range" min="0" step="1000" max="30000" v-model="max"/>
      </li>
      <li>
        <input type="checkbox" id="userLabel" v-model="displayLabel" />
        <label for="userLabel">레벨보기</label>
      </li>
    </ul>
    <!-- 제품카테고리 -->
     <ul class="list">
       <li v-for="(item,index) in filteredProducts" :key="index">
        <ProdctItem :item="item" :cart="cart" @addToCart="addTocart"/>
       </li>
     </ul>
  </div>
</template>

<script>
import ProduData from '@/assets/data.json'
import ProdctItem from '@/components/ProductItem.vue'
import NavPrice from '@/components/NavPrice.vue'

export default {
  data(){
    return {
      displayCart:false,
      cart:[],
      displayLabel:true,
      max:20000,
      products:ProduData 
    }
  },
  components:{ProdctItem,NavPrice},
 computed:{
  filteredProducts(){
    return this.products.filter(item => (item.price < this.max));
  },
  cartTotal(){
    return this.cart.reduce( (inc, item) => Number(item.price) + inc, 0 )
  }

},
 methods:{
   addToCart(product){
     this.cart.push(product);
   }
 }
}
</script>


<style scoped>
body{
  background-color:#666;
}
/* article */
article{
  background-color:#fff;
 padding:0 200px;
 width:1000px;
  margin: 0 auto;
}
/* header */
article>header{
  width:1000px;
  margin: 0 auto;
  border-bottom:1px solid #666;
  padding:10px 20px;
  display:flex;
  justify-content: space-between;
  flex-wrap:wrap;
  align-content: center;
  position:relative;
}
article>header>h3{
  font-size:30px;
  color:#666;
}
article>header>dl{
  display:flex;
  justify-content: flex-end;
  align-items: center;
  
}
article>header dl>dd>ul{
  position:absolute;
  right:0;
  top:50px;
  z-index:100;
  padding:5px 10px;
  border:1px solid #666;
  background-color:#fff;
}
article>header dl>dd>ul>li{
  padding: 10px 0;
  border-bottom:1px solid #666;
}
article>header dl>dd>ul>li:last-child{
  border-bottom:none;
}

/* box */
#box .form{
  padding:30px 0;
  width:1000px;
  margin: 0 auto;
}
#box .form>li{
  margin-bottom:20px;
}
#box .form input{
  border:none;
}

#box .form input[type="range"]{
  width:700px;
}
#box .form label{
  display:inline-block;
  padding:0 20px;
}
/* figure */
#box .list{ 
  border-top:1px dotted #666;
  padding: 0 30px;
}
#box .list>li{
padding:5px 0;
border-bottom:1px dotted #666;
display:flex;
flex-direction: row-reverse;
flex-wrap:wrap;
justify-content: space-between;
}
#box .list>li>p{
  width:100px;
  display:flex;
  justify-content: center;
  align-items: center;
}
#box .list>li>figure{
  width:800px;
  display:flex;
  flex-wrap:wrap;
  justify-content: space-between;
  align-content: flex-start;
}
#box .list>li>figure>img{
  width:150px;
}
#box .list>li>figure>figcaption{
  width:500px;
}

#box .list dd>span.blue{
  color:#fff; 
  background-color:blue; 
  padding:3px; 
  border-radius:4px;}
#box .list dd>span.red{
  color:#fff; 
  background-color:red; 
  padding:3px;
  border-radius:4px;}
#box .list dd>span.green{
  color:#fff; 
  background-color:orange; 
  padding:3px;
  border-radius:4px;}
</style>
