<template>
div class="task-app">
  <h1>Gestor de Tasques</h1>
  <p>This is a simple task management application built with Vue.js.</p>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.title }} - {{ task.completed ? 'Completed' : 'Pending' }}
    </li>
  </ul>

</template>

<script setup>

</script>
