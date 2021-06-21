<template>
    <footer>
        <p>&copy; Tasklist app 2021. All rights unReserved</p>
        <router-link to="/about">About App</router-link>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
}
</script>

<style scoped>
a {
    color: #333;
    font-size: 1.1rem;
}
footer {
    text-align: center;
    margin-top: 20px;
}
</style>