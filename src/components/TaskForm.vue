<template>
    <div class="task-form">
        <input type="text" v-model="title" placeholder="Task title" />
        <input type="date" v-model="dueDate" />
        <button @click="addTask" class="btn-add">Add Task</button>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'TaskForm',
    data() {
        return {
            title: '',
            dueDate: ''
        };
    },
    methods: {
        addTask() {
            const task = {
                title: this.title,
                dueDate: this.dueDate,
                completed: false
            };
            axios.post('http://localhost:3000/api/tasks', task)
                .then(() => {
                    this.$emit('taskAdded'); // Emit event to parent component
                    this.title = ''; // Clear title field after adding task
                    this.dueDate = ''; // Clear dueDate field after adding task
                })
                .catch(error => {
                    console.error('Error adding task:', error);
                });
        }
    }
};
</script>

<style scoped>
.task-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Adding shadow for depth */
}

.task-form input,
.task-form button {
    margin: 5px;
    padding: 10px;
    font-size: 16px;
}

.btn-add {
    background-color: #2196F3;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.btn-add:hover {
    opacity: 0.8;
}
</style>
