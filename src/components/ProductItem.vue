<template>
 <figure>
           <img :src="item.image" :alt="item.name" />
           <figcaption>
             <dl>
               <dt>{{item.name}}</dt>
               <dd>{{item.description}}</dd>
               <dd>레벨</dd>
               <dd>{{item.price}} 원</dd>
             </dl>
           </figcaption>
         </figure>
         <!-- plus -->
         <p>
           <button @click="$emit('addToCart',item)">+</button>
          </p>
</template>

<script>
export default {
props:{
item:{
  type:Object
}
},
emits:[
'addToCart'
]
}
</script>

<style scoped>

</style>