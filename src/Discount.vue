<template>
    <div class="discount">
        <h4>지금 결제하면 {{discount}}% 할인</h4>
        <p class="desc">{{discountDescript}}</p>
    </div>

</template>
<script>
export default {
    name:'Discount',
    props:{ discount:Number,
            discountDescript:String
            }
}
</script>
<style>
.desc{
    color: red;
    
}
</style>

