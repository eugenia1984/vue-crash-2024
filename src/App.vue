<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'pending',
      tasks: ['Task 1', 'Task 2', 'Task 3'],
      link: 'https://google.com'
    }
  }
}
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
  </div>
  <div>
    <p v-if="status === 'active'">User is active.</p>
    <p v-else-if="status === 'pending'">User is pending.</p>
    <p v-else>User is inactive.</p>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }} </li>
    </ul>
    <a v-bind:href="link">Look at Google</a>
  </div>
</template>

