<template>
    <form @submit="onSubmit" action="#" class="addTask">
        <div class="form-control">
            <label for="task">Task: </label>
            <input type="text" v-model="task" name="task" placeholder="eg: Appointment with doctor">
        </div>
        <div class="form-control">
            <label for="day">Date & Time: </label>
            <input type="text" v-model="dateTime" name="dateTime" placeholder="eg:7pm, 23rd march 2021">
        </div>
        <div class="form-control">
            <label for="reminder">Reminder: </label>
            <input type="checkbox" v-model="reminder" name="reminder">
        </div>
        <input type="submit" value="Save Task" class="submitBtn">
    </form>
</template>

<script>
export default {
    name : 'NewTask',
    data() {
        return {
            // setting default form values
            task: '',
            dateTime: '',
            reminder: false,
        }
    },

    methods: {
        onSubmit(event) {
            event.preventDefault();
            if(!this.task || !this.dateTime){
                    console.log('The computer needs info');
                }

            const newTask = {
                id: Math.floor(Math.random() * 100000),
                text: this.task, 
                day: this.dateTime, 
                remind: this.reminder,
            }

            this.$emit('new-task' ,newTask);

            // clear fields after submitting
            this.task = ''
            this.dateTime = ''
            this.reminder = false
        }
    }

}
</script>

<style scoped>
.addTask {
    padding: 10px;
}

.addTask .form-control {
    margin: 10px 0;
}
.addTask input{
    width: 100%;
    border-radius: 5px;
    border: 1px solid #333;
    padding: 8px 10px;
    font-size: 1rem;
    color: #444;
}
.addTask input:focus {
    outline: none;
}
.addTask input[type=checkbox] {
    top: 5px;
    position: relative;
    border: 0;
    width: initial;
    font-size: 1.1rem;
    -webkit-appearance: none;
    width: 40px;
    height: 20px;
    border-radius: 10px;
    transition: .3s ease-in;
    background: #aaa;
    box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2) ;
    margin-left: 5px;
}
.addTask input:checked[type=checkbox] {
    background: rgb(74, 205, 214);
}
.addTask input[type=checkbox]::before {
    position: absolute;
    content: '';
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    top: 0;
    left: 0;
    transform: scale(1.1);
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    transition: .3s ease-in-out;
    cursor: pointer;
}
.addTask input:checked[type=checkbox]::before {
    left: 20px;
}
.addTask .submitBtn {
    border: 0;
    color: #fff;
    background-color: rgb(19, 78, 78);
    cursor: pointer;
}
</style>