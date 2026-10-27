<template>

    <ul v-if="tasks.length > 0">
    <li v-for="task in tasks" :key="task.id">
      <span :class="{ done: task.completed }">{{ task.title }}</span>
      <button @click="emit('toggle', task)">
        {{ task.completed ? 'Completed' : 'Pending' }} 
      </button>
    <button @click="emit('delete',task)" > 🗑 </button> 
    </li>
  </ul>
  <p v-else>No tasks to show.</p>

</template>

<script setup>

const prop = defineProps({
    tasks: {
        type: Array,
        required:true
    }
})

const emit = defineEmits(['toggle', 'delete'])

</script>
