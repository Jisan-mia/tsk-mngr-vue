<template>
  <div :key="task.id" v-for="task in tasks" >
    <SingleTask @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task"/>
  </div>
</template>

<script>
import SingleTask from "./SingleTask.vue"


export default {
  components: { SingleTask },
  name: "Tasks",
  props: {
    tasks: Array,
  },
  emits: ['delete-task', 'toggle-reminder']
}
</script>