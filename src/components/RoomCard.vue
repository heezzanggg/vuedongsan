<template>
  <div>
    <img :src="room.image" class="room-img">
    <!-- <h4 @click="sendData(room.id)">{{ room.title }}</h4> -->
    <h4 @click="$emit('openModal',room.id)">{{ room.title }}</h4>
    <p>{{ room.price }} 원</p>  
  </div>
</template>
<script>
export default{
  name: 'RoomCard',
  props: {
    room : Object,
  },
  data(){
    return{
    }
  },
  methods: {
    sendData(id){
      this.$emit('openModal',id);
    },
  },
}
</script>
<style>
</style>