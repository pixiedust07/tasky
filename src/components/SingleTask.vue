<template>
    <div @dblclick="$emit('toggle-reminder', singleTask.id)" :class="[singleTask.remind ? 'remind' : '', 'task']">
        <div class="task-content">
            <h3>{{ singleTask.text }}</h3>
            <p>{{ singleTask.day }}</p>
        </div>
        <div @click="$emit('remove-task', singleTask.id)" class="delete-icon"><i class="fas fa-trash"></i></div>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        singleTask: Object,
    },
}
</script>

<style scoped>

.task {
    background-color: rgb(214, 243, 245);
    margin: 10px auto;
    padding: 10px 20px;
    border-radius: 5px;
    box-sizing: border-box;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: grab;
}

.task.remind {
    border-top: 5px solid rgb(74, 205, 214);
}

i.fa-trash {
    font-size: 1.2rem;
    color: rgb(235, 86, 86);
    cursor: pointer;
}


</style>