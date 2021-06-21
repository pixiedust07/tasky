<template>
    <div v-show="formTogglerStatus" class="task-form">
        <NewTask @new-task="saveNewTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @remove-task="removeTask" :Tasks="tasks"/>
    <!-- Here the Task is the 'PropName' and tasks is the array returned by the data method -->
</template>

<script>
import Tasks from '../components/Tasks'
import NewTask from '../components/NewTask'

export default {
    name: 'Home',
    props: {
        formTogglerStatus: Boolean,
    },
    components: {
        Tasks,
        NewTask,
    },
    data() {
        return {
            tasks: [],
        }
    },
    methods: {
    async saveNewTask(newTask) {
      const res = await fetch('api/tasks/', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(newTask)
      })

      const data = await res.json()
      // here we redefine our existing tasks array by selecting all previous objects and appending new task along with them.
      this.tasks = [...this.tasks, data ]
    },
    // how did id have access to the tasks without passing it on calling
    // because it's passed on emiting from the Tasks component 
    async removeTask(id) {
      if(confirm('Are you sure ?')) {
        const res = await fetch(`api/tasks/${id}`, {
        method: 'DELETE',
      })

        res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : alert('Error on deleting task')
      }

      
    },
    async toggleReminder(id) {
      const taskToToggleReminder = await this.fetchTask(id)
      const updateReminder = {...taskToToggleReminder, remind: !taskToToggleReminder.remind}

      const res = await fetch(`api/tasks/${id}`,{
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updateReminder)
      })

      const data = await res.json()
      this.tasks = this.tasks.map(task => task.id === id ? { ...task, remind: data.remind} : task)
      // here the spread operator points to the initial values of the object upto the remind key
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')
      const data = await res.json()
      return data
    },
    async fetchTask(taskId) {
      const res = await fetch(`api/tasks/${taskId}`)
      const data = await res.json()
      return data
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  }
}
</script>