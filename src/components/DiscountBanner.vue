<template>
  <div class="discount-banner">
    <h4>지금 결제하면 {{ countDown }}% 할인</h4>
  </div>  
</template>
<script>
export default{
  name:'DiscountBanner',
  data(){
    return{
      initialCount: 10,
    }
  },
  computed:{
    countDown(){
      return this.initialCount;
    },
  },
  mounted(){
    const intervlaId = setInterval(()=>{
      if(this.initialCount > 0){
        this.initialCount -= 1;
      }else{
        clearInterval(intervlaId);
      }  
    },100);
  },
}
</script>
<style>
</style>