<template>
    <div v-for="(name,index) in products" :key="index">
    <img class="room-img" 
        :src="products[index].image" 
        @click="$emit('modalOpenPlease',index);">
    <h4>{{index+1}}번째 : {{products[index].title}}</h4>
    <p>{{products[index].price}} 만원</p> 
  </div>
</template>
<script>
export default {
    name:'Card',
    props:{ products:Array,
            modalOpen:Boolean}
    
}
</script>