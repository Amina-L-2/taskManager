<template>
<div class="task-app">
  <h1>Gestor de Tasques</h1>

  <TaskForm
    @add="addTask" 
  />
  
  <br/><br/>

  <input type="checkbox" id="filter" v-model="showOnlyPending" /> 
  <label for="filter"> Just the pending tasks</label>
  
  <br/><br/>
  
  <TaskList
    :tasks="filteredTasks"
    @toggle="changeStatus"
    @delete="deleteTask"
  />

  <br/><br/>

  <p> Total: {{ tasks.length }} | Pending: {{ pendingTasksCount }}</p>

</div>

</template>

<script setup>
import { ref, computed, watch } from 'vue'
import TaskList from './TaskList.vue'
import TaskForm from './TaskForm.vue'

const showOnlyPending = ref(false)

const defaultTasks = [
  { id: 1, title: 'Learn Vue.js', completed: false },
  { id: 2, title: 'Go for a walk', completed: true },
  { id: 3, title: 'Prep Test', completed: false },
  { id: 4, title: 'Go to gym', completed: true },
  { id: 5, title: 'Study - optional ;)', completed: false }
]

// Load saved tasks safely and show default tasks if storage is empty 
const loadTasks = () => {
  try {
    const saved = JSON.parse(localStorage.getItem('tasks'))
    if (Array.isArray(saved)) return saved
  } 
  catch (e) {
  }
  return defaultTasks
}

const tasks = ref(loadTasks())

// Unique id for tasks
let nextId = Math.max(0, ...tasks.value.map(task => task.id)) + 1

const filteredTasks = computed(() => {
  if(showOnlyPending.value) {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})


const addTask = (title) => {
  tasks.value.push({
    id: nextId++,
    title,
    completed: false
  })
}
const deleteTask = (tasktodelete) => {
  tasks.value = tasks.value.filter(
    task => task.id !== tasktodelete.id
  )
}

const changeStatus = (taskToChange) => {
  taskToChange.completed = !taskToChange.completed
}

const pendingTasksCount = computed(() => {
  return tasks.value.filter(task => !task.completed).length
})

//saves the task for a session
watch(
  tasks, (newTasks) => {
    localStorage.setItem('tasks', JSON.stringify(newTasks))
  },
  { deep: true}
)
</script>
