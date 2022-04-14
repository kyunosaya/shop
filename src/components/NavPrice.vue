<template>
<div id="header">
    <h3>제품카테고리</h3>
    <dl>
      <dt>구매상품 총</dt>
      <dd>{{cartTotal}} 원 </dd>
      <dd><button @click="displayCart = !displayCart">
        장바구니보기 {{cart.length}}</button>
        <ul v-if="displayCart">
        <li v-for="(item,index) in cart" :key="index">
          {{item.name}} : {{item.price}}원
        </li>
        </ul>
      </dd>
    </dl>
  </div>
</template>

<script>
export default {
  data(){
    return{
      displayCart:false,
    }
  },
  props:['cart'],
  computed:{
    cartTotal(){
    return this.cart.reduce( (inc, item) => Number(item.price) + inc, 0 )
  }
  }
}
</script>

<style scoped>

</style>