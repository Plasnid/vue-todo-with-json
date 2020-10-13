<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>{{showCompletion}}</h1>
    <ToDo :todos="tasks" @comp-change="toDoStatus" @del-entry="deleteEntry"/>
    <TaskForm :todos="tasks" />
  </div>
</template>

<script>
import ToDo from './components/Todo.vue'
import TaskForm from './components/TaskForm.vue'
import stuffToDo from '@/assets/data.json'

export default {
  name: 'App',
  components: {
    ToDo,
    TaskForm
  },
  data: function(){
    return {
      showCompletion: "",
      tasks: stuffToDo.tasks
    }
  },
  mounted: function(){
    console.log(this.tasks);
    this.tasks = stuffToDo.tasks;
  },
  methods: {
    toDoStatus() {
      let tasksDone = this.tasks.every(val => val.status==true);
      if(tasksDone==true){
        this.showCompletion = "All Done";
      }else{
        this.showCompletion = "More stuff to do!";
      }
    },
    deleteEntry(key){
      this.tasks.splice(key,1);
    }
  },
  watch: {
    tasks() {
      this.toDoStatus();
    },
  },
  created: function(){
    /**
     * otherhooks include beforeCreate, beforeMount, mounted, beforeUpdate, updated, beforeDestroy, and destroyed
     * https://vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks
     */
    this.toDoStatus();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
