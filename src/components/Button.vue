<template>
  <button @click="addTask()" :style="{background: color}" class="btn"> {{text}} </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    text: String,
    color: String,
    showAddTask: Boolean
  },
  methods: {
    addTask() {
      this.$emit('btn-click')
    }
  }
}
</script>