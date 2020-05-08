<template>
<div>
    <div class='content-todo' v-show='!isEditing'>
        <h2>{{ todo.title }}</h2>
        <ul v-if="todo.projects.length">
            <li v-for='project in todo.projects' :key='project.id'>
                <span v-bind:class='{done: project.completed}'>
                    <strong>{{ project.id }}</strong>
                    {{ project.task }}
                </span>
            </li>
        </ul>
        <div class='buttons'>
            <button class='delete-todo' v-on:click='$emit("remove-todo", todo.id)'>Удалить</button>
            <button class='change-todo' v-on:click='showForm'>Изменить</button>
        </div>
    </div>
    <!-- Блок для редактирования дел -->
    <div class='content-todo content-change' v-show='isEditing'>
        <div class='field'>
            <label>Заголовок:</label>
            <input type='text' v-model="todo.title">
        </div>
        <div class='field' v-for="projects of todo.projects" :key="projects.id">
            <label>Задача:</label>
            <input v-model="projects.completed" type='checkbox' ref='projects' defaultValue="">
            <input type='text' v-model="projects.task">
        </div>
        <button class='change-todo' v-on:click='saveTodo'>Сохранить / Закрыть</button>
        <button class='change-todo' v-on:click='createProject'>Добавить дело</button>
    </div>
</div>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number,
    },
    data() {
        return {
            isEditing: false,
            newTodo: this.todo
        }
    },
    methods: {
        // Метод связан с AddTodo, что бы была возможность редактировать список задач
        createProject() {
            const id = this.todo.projects.length + 1
            this.todo.projects.push({
                id,
                task: '',
                completed: false
            })
        },
        // При нажатии появляется блок с возможностью редактировать блок
        showForm() {
            this.isEditing = true;
        },
        // Сохраняет блок с делами и закрывает его
        saveTodo() {
            this.$root.$emit('save-todos', this.newTodo)
            this.isEditing = false
        }
    }
}
</script>

<style scoped>
.content-todo {
    max-width: 600px;
    margin: auto;
    margin-bottom: 20px;
    padding-bottom: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
}

.content-change {
    margin-top: 20px;
    padding-top: 20px;
}

ul {
    list-style: none;
    margin: 0px;
    padding: 0px;
}

li {
    border-bottom: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding-bottom: 10px;
    margin-bottom: 20px;
}

input {
    margin-right: 1rem;
}

.buttons {
    max-width: 150px;
    display: flex;
    justify-content: space-between;
    margin: auto;
}

.done {
    text-decoration: line-through;
}

.delete-todo {
    border: 1px solid #ff0000;
    color: #ff0000;
    cursor: pointer;
}

.delete-todo:hover {
    background: #ff0000;
    color: #fff;
}

.change-todo {
    border: 1px solid #00ff09;
    color: #00ff09;
    cursor: pointer;
}

.change-todo:hover {
    background: #00ff09;
    color: #fff;
}

input {
    margin-bottom: 10px;
}
</style>
