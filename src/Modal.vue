<template>
    <div class="black-bg" v-if="modalOpen == true">
        <div class="white-bg">
            <img :src="products[idx].image" style="width:100%">
            <h4>{{ products[idx].title }}</h4>
            <p>{{ products[idx].content }}</p>
            개월수 : <input id="month" @input="month=$event.target.value"/><br>
            현자산 : <input id="asset" v-model="asset"/>

            <p>{{month}}개월 신청 시 {{ products[idx].price * month}} 원</p>
            <p>집사고남은돈 : {{asset - products[idx].price * month}}</p>
            <button @click="$emit('close')">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
    name:'Modal', 
    props:{products:Array,
        modalOpen:Boolean,
        idx:Number},
    data(){
        return{
            month:'1',
            asset:1000000
        }
    },
    watch : {
        month(keyword) {
            if(keyword>=13 || keyword<=0){
                alert('1~12사이의 숫자를 입력하세요');
                document.getElementById('month').value = 1;
                this.month ='1';
                return false;
            }

            if(!(/^[0-9]+$/).test(keyword)){
                alert('숫자만 입력하시오');
                document.getElementById('month').value = 1
                this.month = '';
                return false;
            }
        }
    }


}
</script>

<style>


</style>