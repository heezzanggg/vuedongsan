<template>
  <!-- <div class="start" :class="{end: isModalOpen}">
    <RoomModal
      :roomData="roomData" 
      :roomNumber="selectedRoomNumber"
      :isModalOpen="isModalOpen"
      @closeModal="closeModal"
    />
  </div> -->
  <Transition name="fade">
    <RoomModal 
      :roomData="roomData" 
      :roomNumber="selectedRoomNumber"
      :isModalOpen="isModalOpen"
      @closeModal="closeModal"
    />
  </Transition>
  <DiscountBanner v-if="this.isBannerVisiable"/>
  <!-- 메인페이지 방문하자마자 30%라고 적힌 할인문구 1초마다 1% 감소하는거 만들기 -->
  <button @click="sortAscByPrice">sortAscByPrice</button>
  <button @click="sortDescByPrice">sortDescByPrice</button>
  <button @click="sortAscByTitle">sortAscByTitle</button>
  <button @click="sortDescByTitle">sortDescByTitle</button>

  <div class="menu">
    <a v-for="(menu,index) in menuItems" :key="index">{{ menu }}</a>
  </div>
  <!-- <RoomCard  
    v-for="(room,i) in roomData" :key="i"
    :room="room"
    @openModal="openModal"
  /> -->
  <RoomCard  
    v-for="(room,i) in roomData" :key="i"
    :room="room"
    @openModal="this.selectedRoomNumber = $event ; isModalOpen=true"
  />
</template>

<script>
import roomData from "./assets/oneroom.js"
import DiscountBanner from "./components/DiscountBanner.vue";
import RoomModal from "./components/RoomModal.vue";
import RoomCard from "./components/RoomCard.vue";
export default {
  name: 'App',
  data(){
    return{
      roomData : roomData,
      menuItems: ['Home','Shop','About'],
      price1: 60,
      price2: 70,
      products: ['역삼동원룸','천호동원룸','마포구원룸'],
      complaintCounts: [0,0,0],
      isModalOpen: false,
      selectedRoomNumber: 0,
      isBannerVisiable:true,
    }
  },
  methods: {
    checkOpCdAndStat(arr) {
      // 배열을 순회하면서 조건을 확인
      for (const item of arr) {
        if (item.opCd !== '060' || item.opStatCd !== '001') {
          // 하나라도 조건을 충족하지 않으면 false 반환
          return false;
        }
      }
      // 모든 객체가 조건을 충족하면 true 반환
      return true;
    },
    sortDescByTitle(){
      //문자정렬 : localeCompare
      this.roomData.sort((a,b) => b.title.localeCompare(a.title))
    },
    sortAscByTitle(){
      this.roomData.sort((a,b) => a.title.localeCompare(b.title))
    },
    sortDescByPrice(){
      this.roomData.sort((a,b)=> b.price - a.price)
    },
    sortAscByPrice(){
      //숫자정렬 : -
      this.roomData.sort((a,b) => {
        return a.price-b.price;
      })
    },
    increaseComplaintCount(i){
      this.complaintCounts[i]++;
    },
    openModal(id){
      this.selectedRoomNumber = id;
      this.isModalOpen = true;
    },
    closeModal(){
      this.isModalOpen = false;
    },
  },
  mounted(){
    setInterval(()=>{
      //접속 10초 후  배너 사라짐
      this.isBannerVisiable = false;
    },10000);
  },
  components: {
    DiscountBanner :DiscountBanner,
    RoomModal :RoomModal,
    RoomCard :RoomCard,
},
}
</script>

<style>
.start{
  opacity: 0;
  transition: all 1s;
}
.end{
  opacity: 1;
}
.fade-enter-from{
  /* 등장 애니메이션, 시작 스타일 */
  opacity: 0;
}
.fade-enter-active{
  /* transition */
  transition:all 1s;
}
.fade-enter-to{
  /* 등장 애니메이션, 종료 스타일 */
  opacity: 1;
}
.fade-leave-from{
  /* 퇴장 애니메이션, 시작 스타일 */
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  /* 퇴장 애니메이션, 종료 스타일 */
  opacity: 0;
}
body{
  margin: 0;
}
div{
  box-sizing: border-box;
}
.discount-banner{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border: 5px;
}
.black-bg{
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
