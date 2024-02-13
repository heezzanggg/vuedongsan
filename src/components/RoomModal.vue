<template>
  <div class="black-bg" v-if="isModalOpen === true">
    <div class="white-bg">
      <img :src="roomData[roomNumber].image" class="room-img">
      <h4>{{ roomData[roomNumber].title }}</h4>
      <p>{{ roomData[roomNumber].content }}</p>
      <input v-model="month"> 
      <p>{{month}} 개월 : {{ roomData[roomNumber].price * month }} 원</p>
      <button @click="closeModal">닫기</button>
    </div>
  </div>
    <!-- 모달창내에 input이 있는데 여기에 2를 기입했을때 알림창 alert()띄우기 : lifecycleHook 이용해서 -->
</template>
<script>
export default{
  name: 'RoomModal',
  props: {
    roomData : Array,
    roomNumber : Number,
    isModalOpen : Boolean,
  },
  data(){
    return{
      month:1,
    }
  },
  watch:{
    month(afterVal,beforeVal){
      // console.log("after",afterVal)
      console.log("beforeVal",beforeVal)
      if(afterVal >= 13){
        alert('13이상 입력 불가');
        this.month = 1;
      }
      if(isNaN(afterVal) === true){
        alert('숫자만 가능함');
        this.month = 1;
      }
    },
  },
  methods: {
    closeModal(){
      this.$emit('closeModal');
    },
  },
  beforeUpdate(){
    console.log(this.month);
    console.log("beforeUpdate");
    console.log(this.month);
    if(this.month == 2){
      alert("2입력함");
      this.month = 3;
    }
  },
  updated(){
    console.log(this.month);
    console.log("update");
    console.log(this.month);
    if(this.month == 9){
      alert("9입력");
      this.month = 4;
    }
  },
}
</script>
<style></style>