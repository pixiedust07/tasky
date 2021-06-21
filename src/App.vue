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
    saveNewTask(newTask) {
      // here we redefine our existing tasks array by selecting all previous objects and appending new task along with them.
      this.tasks = [...this.tasks, newTask ]
    },
    // how did id have access to the tasks without passing it on calling
    // because it's passed on emiting from the Tasks component 
    removeTask(id) {
      if(confirm('Are you sure? '))
        this.tasks = this.tasks.filter(task => task.id !== id)
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task => task.id === id ? { ...task, remind: !task.remind } : task)
      // here the spread operator points to the initial values of the object upto the remind key
    }
  },
  created() {
    this.tasks = [
      {
        id: 1, 
        text: 'Take out trash', 
        day: '21st march 2021',
        remind: true,
      },
      
      {
        id: 2, 
        text: 'Appointment at clinic', 
        day: '21st june 2021',
        remind: true,
      },

      {
        id: 3, 
        text: 'Visit Park', 
        day: '3rd july 2021',
        remind: false,
      }
    ]
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
