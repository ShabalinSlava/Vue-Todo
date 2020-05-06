<template>
<div>
    <TodoItem v-for="todo of todos" v-bind:todo='todo' v-on:remove-todo='removeTodo' />
</div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
export default {
    props: ['todos'],
    components: {
        TodoItem,
    },
    methods: {
        removeTodo(id) {
            this.$emit('remove-todo', id)
        }
    }
};
</script>

<style scoped>
ul {
    list-style: none;
    margin: 0;
    padding: 0;
}
</style>
