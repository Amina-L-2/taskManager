<template>

  <form @submit.prevent="submitTask">
    <input v-model="newTask" placeholder="Add a new task" />
    <button type="submit">Add Task</button>
  </form>

</template>

<script setup>

import { ref } from 'vue'

const emit = defineEmits(['add'])
const newTask = ref('')

const submitTask = () => {
  const title = newTask.value.trim()
  if (!title) return

  emit('add', title)
  newTask.value = ''
}

</script>