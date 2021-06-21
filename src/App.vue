<template>
  <div class="container">
    <Header @toggle-form="toggleForm" title="Task Tracker App" :formTogglerStatus="showAddTask"/>
    <div v-show="showAddTask" class="task-form">
      <NewTask @new-task="saveNewTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @remove-task="removeTask" :Tasks="tasks"/>
    <!-- Here the Task is the 'PropName' and tasks is the array returned by the data method -->
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import NewTask from './components/NewTask'


export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    NewTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false, 
    }
  },
  methods: {
    toggleForm() {
      this.showAddTask = !this.showAddTask
    },
    async saveNewTask(newTask) {
      const res = await fetch('api/tasks/', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(newTask)
      })

      const data = res.json()
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
      console.log(data);
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

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
  /* background-color: #222; */
}
.btn {
  display: inline-block;
  background: rgb(20, 20, 20);
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
