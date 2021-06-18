<template>
    <button @click="addTask" class="btn" :style="{background: color}">{{ btnTitle }}</button>
</template>

<script>
export default {
    name: 'Button', 
    props: {
        btnTitle: String,
        color: String,
    },
    methods: {
        addTask() {
            console.log('Task Added successfully');
        }
    }
}
</script>