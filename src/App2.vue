<script setup>
  import { ref } from 'vue';

  const name = ref('John Doe');
  const tasks = ref([
    {name: 'Task One', completed: false},
    {name: 'Task Two', completed: false},
    {name: 'Task Three', completed: false},
  ]);
  const status = ref(true);
  const newTask = ref('');

  function toggleStatus(status){
    this.name = status ? 'Benchanan Idehen' : 'Dumebi Idehen'
  }

  function addTask(){
    if(newTask.value.trim() === '')
        return alert('Input Empty!');
    else
      tasks.value.push({name: newTask.value, completed: false});
  }

  function deleteTask(){

  }
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === true">User is active</p>
  <p v-else-if="status === false">User is pending</p>
  <p v-else>User is In active</p>

  <form @submit.prevent="addTask">
    <label for="add">Add Task</label>
    <input id="add" type="text" v-model="newTask"/>

    <button type="submit">Submit</button>
  </form>

  <header>To do Tasks: </header>
  <ul v-for="(task, idx) in tasks.filter((value) => !value.completed)" :key="idx">
    <li>{{ task.name }}</li>
    <input type="checkbox" v-model="task.completed" :name="task.name"/>
  </ul>

  <header>Complete Tasks: </header>
  <ul v-for="(task, idx) in tasks.filter((value) => value.completed)" :key="idx">
    <li>{{ task.name }}</li>
  </ul>

  <button @click="toggleStatus(false)">Click Me</button>
</template>
