<template>
    <header>
        <h1>{{ title }}</h1>
        <Button btnTitle="Add new task" color="rgb(68 193 91)"/>
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: "Header",
    props: {
        title: {
            type: String,
            default: "Task Lister App",
        },
    },
    components: {
        Button,
    }

}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>