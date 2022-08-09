<template>
  

  <!-- 데이터 보내주기 -->
  <div class="start" :class={end:modalOpen}> 
    <Modal :products="products" 
          :modalOpen="modalOpen"
          :idx="idx"
          @close="modalOpen=false"
    />
  </div>
  <div class="menu">
    <a v-for="(name,idx) in menu" :key="idx">
      {{menu[idx]}}
    </a>
  </div>  
  <Discount v-if="showDiscount==true" 
            :discount="discount"
            :discountDescript="discountDescript"

            />
  <div>
    <button @click="priceSort">낮은가격순</button>
    <button @click="sortBack">원래대로</button>
  </div>
  <p></p>
  <Card :products="products" 
        :modalOpen="modalOpen" 
        @modalOpenPlease="modalOpen=true,
                          idx=$event"
  />
</template>
<script>
import rooms from "./roomData.js";
import Discount from "./Discount.vue";
import Modal from "./Modal.vue"
import Card from "./Card.vue"

export default {
  name: 'App',
  data(){ // 데이터 보관함, 즉 변수들 다 여기다 보관함 (객체 형태로 저장)

    return{
      menu : ['Home','Products','About'],
      claimCount : [0,0,0], // claimCnt - arrayOfProducst
      products : rooms, 
      modalOpen :false,
      idx : 0, //초기화
      productsOriginal : [...rooms],
      showDiscount : true,
      discount : 20,
      discountDescript : '',
      
    }
  },
  components: {
    Discount,
    Modal,
    Card
  },
  mounted() {
    // 1초마다 할인율 감소
    setInterval(()=>{
      this.discount--;
      if(this.discount==10){
        this.discountDescript = '할인마감임박';
      }
      if(this.discount==0){
        this.showDiscount = false;
      }
    },1000)
  },

  methods : {
    increase(index) {
      if(index==0){
        this.claimCount[0]++;
      } else if(index==1){
        this.claimCount[1]++;
      } else if(index==2){
        this.claimCount[2]++;
      }
    },

    priceSort(){
      this.products.sort(function(a,b){
        return a.price - b.price;
      });
    },

    sortBack(){
      this.products = [...this.productsOriginal];
    },

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

.menu {
  background : darkslateblue;
  padding : 15px;
  border-radius : 5px;
}
.menu a {
  color : white;
  padding : 10px;
}

.room-img {
  width:50%;height: 50%;
}

body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 50%; background: white;
  border-radius: 8px;
  padding: 20px;
  margin:auto;
} 
.discount {
  width: 100%; background: #eee;
  border-radius: 5px;
  padding: 10px;
  margin:10px;
}  
.start{
    opacity: 0;
    transition: all 1s;
}

.end{
    opacity: 1;
}
</style>
