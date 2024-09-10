<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'pending',
      tasks: ['Task 1', 'Task 2', 'Task 3'],
      link: 'https://google.com'
    }
  },
  methods: {
    toggleStatus() {
      console.log('toggleStatus')
      if(this.status === 'active') {
        this.status === 'pending'
      } else if (this.status === 'pending') {
        this.status === 'inactive'
      } else {
        this.status === 'active'
      }
    }
  }
};
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
  </div>
  <br />
  <br />
  <div>
    <p v-if="status === 'active'">User is active.</p>
    <p v-else-if="status === 'pending'">User is pending.</p>
    <p v-else>User is inactive.</p>
    <br />
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }} </li>
    </ul>
    <a :href="link">Click for Google</a>
    <br />
    <br />
    <button v-on:click="toggleStatus" >Change status</button>
  </div>
</template>

