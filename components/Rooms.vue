<template>
   <div class="col-md-3 rooms">
       <div class="room" v-for="room in rooms" v-bind:key="room.id" @click="showRoom(room.name)">
           {{room.name}}
       </div>
   <AddRoom /> <!-- Imported AddRoom component -->
   </div>
</template>

<script>
export default {
 name: "Rooms",
 data() {
   return {
       rooms: [
           {id: 1, name: 'PHP Room'},
           {id: 2, name: 'Python Room'},
           {id: 3, name: 'Daily standup'}
       ],
       roomCount: 3, // used to keep track of the number of rooms present
       loading: false, // indicate when tracks in a room is being loaded
   }
 },
 created() {
    $nuxt.$on('new_room', (data) => {
        this.roomCount++;
        this.rooms.push({id: this.roomCount, name: data});
   });
 },
 methods: {
   showRoom(room) {
       $nuxt.$emit('show_room', room);
   }
 }

}
</script>

<style scoped>
   .rooms > .room {
       border: 1px solid rgb(124, 129, 124);
       padding: 13px;
       margin: 3px 0px;
       color: ghostwhite;
   }

   .rooms {
     border: 1px solid rgb(64, 68, 64);
     cursor: pointer;
   }
</style>
