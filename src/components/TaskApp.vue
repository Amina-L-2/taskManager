<template>
<div class="task-app">
  <h1>Gestor de Tasques</h1>
  <input v-model="newTask" placeholder="Add a new task" />
  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.title }} - {{ task.completed ? 'Completed' : 'Pending' }}
    </li>
  </ul>

</div>

</template>

<script setup>
const tasks = [
  { id: 1, title: 'Learn Vue.js', completed: false },
  { id: 2, title: 'Go for a walk', completed: true },
  { id: 3, title: 'Prep Test', completed: false },
];
</script>
