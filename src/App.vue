<template>
<div id="app">
    <h1>{{ title }}</h1>
    <hr>
    <button>Create</button>
    <TodoList v-bind:todos='todos' />
</div>
</template>

<script>
import TodoList from '@/components/TodoList'
export default {
    name: 'App',
    components: {
        TodoList
    },
        data() {
        return {
            title: 'Todo application',
            subtitle: 'Название',
            todos: [
              {title:'Домашние дела', project: 'Купить хлеб', completed: false},
              {title:'Учеба', project: 'Сдать долги', completed: false},
              {title:'Работа', project: 'Сделать тестовое', completed: false},
            ]
        }
    },
    methods: {
      
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
