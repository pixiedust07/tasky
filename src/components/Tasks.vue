<template>
    <div :key="task.id" v-for="task in Tasks">
        <Task @toggle-reminder="$emit('toggle-reminder', task.id)" :singleTask="task" @remove-task="$emit('remove-task', task.id)" />
    </div>
</template>

<script>
import Task from './SingleTask'

export default {
    name: 'Tasks',
    props: {
        Tasks: Array,
    },
    components: {
        Task,
    },
    emits: ['remove-task', 'toggle-reminder']
}
</script>

