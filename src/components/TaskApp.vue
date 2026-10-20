<template>
<div class="task-app">
  <h1>Gestor de Tasques</h1>

  <input v-model="newTask" placeholder="Add a new task" />
  <button @click="addTask" > Add Task</button> 

  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.title }} - {{ task.completed ? 'Completed' : 'Pending' }}
    <button @click="deleteTask(task)" > Delete Task</button> 
    </li>
  </ul>

</div>

</template>

<script setup>
import { ref, watch } from 'vue'

const newTask = ref('')

const tasks = ref(
  JSON.parse(localStorage.getItem('tasks') || 'null') || //to save the tasks even when server is reloaded
  [
    { id: 1, title: 'Learn Vue.js', completed: false  },
    { id: 2, title: 'Go for a walk', completed: true },
    { id: 3, title: 'Prep Test', completed: false }
  ]
)


const addTask = () => {
      if(!newTask.value.trim()) return 

      const taskAdded = {
        id: tasks.value.length + 1,
        title: newTask.value,
        completed: false
      }
      tasks.value.push(taskAdded);
      newTask.value = ''
}

const deleteTask = (tasktodelete) => {
  tasks.value = tasks.value.filter(
    task => task.id !== tasktodelete.id
  )
}

//saves the task for a session
watch(
  tasks, (newTasks) => {
    localStorage.setItem('tasks', JSON.stringify(newTasks))
  },
  { deep: true}
)
</script>
