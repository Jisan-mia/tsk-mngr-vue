<template>
  <header>
    <h1> {{title}} </h1>
    <span >
    <Button v-show="homePage" @btn-click="$emit('toggle-add-task')" :color="showAddTask ? 'red' : 'green' " :text="showAddTask ? 'Close' : 'Add Task' "/>
    </span>
    
  </header>
</template>

<script>
import Button from './Button'
 export default {
   name: "Header",
   props: {
     title: String,
     showAddTask: Boolean,
   },
   components: {
     Button
   },
   computed: {
     homePage() {
       if(this.$route.path === '/') {
         return true
       } else {
         false
       }
     }
   }
  //  emits: ['toggle-add-task']
 }
 
</script>

<style scoped>
header{
  display: flex;
  justify-content: space-between;
  align-content: center;
  margin-bottom: 20px;
}
</style>