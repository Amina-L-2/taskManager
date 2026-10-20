<template>
<div class="task-app">
  <h1>Gestor de Tasques</h1>

  <input v-model="newTask" placeholder="Add a new task" />
  <button @click="addTask" > Add Task</button> 
  
  <br/><br/>

  <input type="checkbox" id="filter" v-model="showOnlyPending" /> 
  <label for="filter"> Just the pending tasks</label>
  
  <br/><br/>
  
  <ul>
    <li v-for="task in filteredTasks" :key="task.id">
      <span :class="{ done: task.completed }">{{ task.title }}</span>
      <button @click="changeStatus(task)">
        {{ task.completed ? 'Completed' : 'Pending' }} 
      </button>
    <button @click="deleteTask(task)" > 🗑 </button> 
    </li>
  </ul>

  <br/><br/>
  <p> Total: {{ tasks.length }} | Pending: {{ pendingTasksCount }}</p>

</div>

</template>

<script setup>
import { ref, computed, watch } from 'vue'

const newTask = ref('')
const showOnlyPending = ref(false)

const tasks = ref(
  JSON.parse(localStorage.getItem('tasks') || 'null') || //to save the tasks even when server is reloaded
  [
    { id: 1, title: 'Learn Vue.js  ', completed: false  },
    { id: 2, title: 'Go for a walk  ', completed: true },
    { id: 3, title: 'Prep Test', completed: false },
    { id: 4, title: 'Go to gym', completed: true },
    { id: 5, title: 'Study - optional ;) ', completed: false }
  ]
)

const filteredTasks = computed(() => {
  if(showOnlyPending.value) {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})

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
