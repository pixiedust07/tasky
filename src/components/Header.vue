<template>
    <header>
        <h1>{{ title }}</h1>
        <Button btnTitle="Add new task" color="#134e4e"/>
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
header h1 {
    color: rgb(19, 78, 78);
}
</style>