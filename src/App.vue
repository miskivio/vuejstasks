<template>

<div class="container">
  <Header @toggle-add-task ="toggleAddTask" title = "Task Tracker" :showAddTask ="showAddTask"/>
  <div v-show="showAddTask">
  <AddTask @add-task = "addTask"/>
  </div>

  <Tasks @toggle-reminder = "toggleReminder" @delete-task = "deleteTask" :tasks = "tasks"/>
</div>

</template>

<script>

import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: true
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },

    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
   
    deleteTask(id) {
      if(confirm('Do you really want to delete this one?')) {
          this.tasks = this.tasks.filter((task) => task.id !== id)
        }
    },

toggleReminder (id) {
  this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
},

async fetchTasks () {
    const res = await fetch('http://localhost:5000/tasks')
    const data = await res.json()
    return data
  },
async created () {
  this.tasks =  await this.fetchTasks()
}
  },
  
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
