<template>
  <div class="container">
    <Header title="Task Tracker App"/>
  </div>
</template>

<script>
import Header from './components/Header'


export default {
  name: 'App',
  components: {
    Header,
  },
  data() {
    return {
      tasks: [],
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
        id: 1, 
        text: 'Visit Park', 
        day: '3rd july 2021',
        remind: false,
      },

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
