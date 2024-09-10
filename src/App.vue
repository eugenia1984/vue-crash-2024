<script setup>
import { ref } from 'vue';

// COMPOSITION de la forma mas corta
  const name = ref('John Doe');
  const status = ref('active');
  const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
  const newTask = ref(''); 

  const toggleStatus = () => {
    console.log('toggleStatus')
    if(status.value === 'active') {
      status.value === 'pending'
    } else if (status.value === 'pending') {
      status.value === 'inactive'
    } else {
      status.value === 'active'
    } 
  }

  const addTask = () => {
    // If there is a value for newTask, then add new task
    if(newTask.value.trim() !== '') {
      tasks.value.push(newTask.value);
      // Reset the newTaskValue to be able to add a new one
      newTask.value = '';
    } 
  }

  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  }

</script>

<template>
  <div>
    <h1>{{ name }}</h1>
  </div>
  <br />
  <div>
    <p v-if="status === 'active'">User is active.</p>
    <p v-else-if="status === 'pending'">User is pending.</p>
    <p v-else>User is inactive.</p>
    <br />
    <form @submit.prevent="addTask">
      <label for="newTask">Add Task: </label>
      <input type="text" id="newTask" name="newTask" v-model="newTask"/>
      <button type="submit">Submit</button>
    </form>
    <br />
    <h3>Tasks:</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span class="task-item-name">
          {{ task }}
        </span> 
        <button @click="deleteTask(index)">X</button> 
      </li>
    </ul>
    <br />
     <button @click="toggleStatus" type="button" >Change status</button>
  </div>
</template>

<style scoped>
label,
input {
  display: block;
  margin-bottom: 0.5rem;
}

li {
  margin-bottom: 0.5rem;
}

.task-item-name {
  padding-right: 0.75rem;
}
</style>

