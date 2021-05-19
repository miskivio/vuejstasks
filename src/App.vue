<template>

<div class="container">
  <Header title = "Task Tracker"/>
  <Tasks @delete-task = "deleteTask" :tasks = "tasks"/>
</div>

</template>

<script>

import Header from './components/Header'
import Tasks from './components/Tasks'
export default {
  name: 'App',
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
   
deleteTask(id) {
   if(confirm('Do you really want to delete this one?')) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }
}
  },
  created() {
    this.tasks = [
     {
      id :1,
      text:'123',
      day:'2 days left',
      reminder: true
     },
     {
      id :2,
      text:'421321',
      day:'2 days left',
      reminder: false
     },
     {
      id :3,
      text:'421321',
      day:'2 days left',
      reminder: true
     },
    ]
  }
}

</script>

<style>
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
  border:1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
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



</style>
