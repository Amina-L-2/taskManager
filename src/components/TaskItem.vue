<template>

    <li>
        <span :class="{ done: task.completed }">{{ task.title }}</span>
        <button @click="emit('toggle', task)">
            {{ task.completed ? 'Completed' : 'Pending' }}
        </button>
        <button @click="emit('delete', task)"> 🗑 </button>
    </li>

</template>

<script setup>

const props = defineProps({
    task: {
        type: Object
    }
})

const emit = defineEmits(['toggle', 'delete'])

</script>