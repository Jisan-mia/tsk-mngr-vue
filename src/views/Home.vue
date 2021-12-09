<template>

    <AddTask  v-show="showAddTask" @add-task='addTask' />
    <Tasks @toggle-reminder="toggleTask" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
  import AddTask from '../components/AddTask.vue'
  import Tasks from '../components/Tasks.vue'

  export default {
    name: 'Home',
    props: {
      showAddTask: Boolean
    },
    components: {
      Tasks,
      AddTask,
    },
    data() {
      return {
        tasks: []
      }
    },
    methods: {
      
      async addTask(newTask) {
        const res = await fetch('api/tasks', {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(newTask)
        })

        const data = await res.json();

        this.tasks = [...this.tasks, data]
      },
      async deleteTask(id) {
        const res = await fetch(`api/tasks/${id}`,{
          method: 'DELETE',
        })

        res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : alert('Error deleting task')
        
      },
      async toggleTask(id){
        const taskToToggle = await this.fetchSingleTask(id);

        const updateTask = {
          ...taskToToggle,
          reminder: !taskToToggle.reminder
        }
        const res = await fetch(`api/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-type': 'application/json'
          },
          body: JSON.stringify(updateTask)
        } )

        const data = await res.json()


        this.tasks = this.tasks.map(task => {
          if(task.id === id) {
            return {...task, reminder: data.reminder}
          }
          return task
        })
      },
      async fetchTasks() {
        const res = await fetch('api/tasks');
        const data = await res.json();
        return data;
      },

      async fetchSingleTask(id) {
        const res = await fetch(`api/tasks/${id}`)
        const data = await res.json();
        return data;
      }
    },
    async created() {
      this.tasks = await this.fetchTasks()
    }
  
  }
</script>