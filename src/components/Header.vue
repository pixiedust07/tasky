<template>
    <header>
        <h1>{{ title }}</h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-form')" :btnTitle="formTogglerStatus ? 'Close' : 'Add new task' " :color="formTogglerStatus ? 'red' : '#134e4e' "/>
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
        formTogglerStatus: {
            type: Boolean, 
        },
    },
    components: {
        Button,
    },
    computed: {
        homePage() {
            if(this.$route.path === '/') {
                return true
            } else {
                return false
            }
        }
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