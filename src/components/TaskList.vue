<template>

    <ul v-if="tasks.length > 0">
        <TaskItem
            v-for="task in tasks"
            :key="task.id"
            :task="task"
            @toggle="emit('toggle', $event)"
            @delete="emit('delete', $event)"
        />
    </ul>
    <p v-else>No tasks to show.</p>

</template>

<script setup>
import TaskItem from './TaskItem.vue';


const prop = defineProps({
    tasks: {
        type: Array
    }
})

const emit = defineEmits(['toggle', 'delete'])

</script>
