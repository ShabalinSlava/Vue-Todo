<template>
<li>
    <span v-bind:class='{done: todo.completed}'>
        <input type='checkbox' v-on:change='todo.completed = !todo.completed' />
        <strong>{{ todo.id }}</strong>
        {{ todo.project }}
    </span>
</li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>
li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 1rem;
}

input {
    margin-right: 1rem;
}

.done {
    text-decoration: line-through;
}
</style>
