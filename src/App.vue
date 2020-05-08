<template>
<div id="app">
    <h1>{{ title }}</h1>
    <hr>
    <AddTodo @add-todo='addTodo' />
    <TodoList v-bind:todos='todos' @remove-todo='removeTodo' v-if='todos.length' />
    <p v-else>Нет заметок!</p>
</div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
    name: 'App',
    components: {
        TodoList,
        AddTodo
    },
    data() {
        return {
            title: 'Todo application',
            todos: []
        }
    },
    created() {
        this.$root.$on('save-todos', this.saveTodo)
    },
    mounted() {
        if (JSON.parse(localStorage.getItem('todos'))) {
            this.todos = JSON.parse(localStorage.getItem('todos'))
        }

    },
    methods: {
        // Сохранение при перезагрузки страницы
        saveTodo(updatedTodo) {
            this.todos[updatedTodo.id - 1] = updatedTodo
            localStorage.setItem('todos', JSON.stringify(this.todos))
        },
        // Удаление
        removeTodo(id) {
            if (this.todos.length > 1) {
                this.todos = this.todos.filter(t => t.id !== id)
            }
            this.todos = []
            localStorage.setItem('todos', JSON.stringify(this.todos))
        },
        // Добавление
        addTodo(todo) {
            todo['id'] = this.todos.length + 1
            this.todos.push(todo)
            localStorage.setItem('todos', JSON.stringify(this.todos))
        }
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
