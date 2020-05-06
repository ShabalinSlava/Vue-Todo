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
            todos: [{
                    id: 1,
                    title: 'Домашние дела',
                    project: 'Купить хлеб',
                    completed: false
                },
                {
                    id: 2,
                    title: 'Учеба',
                    project: 'Сдать долги',
                    completed: false
                },
                {
                    id: 3,
                    title: 'Работа',
                    project: 'Сделать тестовое',
                    completed: false
                },
            ]
        }
    },
    methods: {
      removeTodo(id) {
        this.todos = this.todos.filter(t => t.id !== id)
      },
      addTodo(title) {
        this.todos.push(title)
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
