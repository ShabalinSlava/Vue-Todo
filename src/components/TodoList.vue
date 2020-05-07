<template>
<div>
    <TodoItem v-for='(todo, i) of todos' :todo='todo' :key="todo.id" :index='i'  @remove-todo='changeCofirmDelete' />
    <div class="dialog" v-if="removedTodoId">
        Подтвердить удаление
        <button class="confirm" @click="removeTodo">Подтвердить</button>
        <button class="cancled"  @click="removedTodoId = null;dialog = !dialog">Отмена</button>
    </div>
</div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
export default {
    props: ['todos'],
    components: {
        TodoItem,
    },
    data() {
        return {
            removedTodoId: null,
            dialog: false
        }
    },
    methods: {
        changeCofirmDelete(id) {
            this.removedTodoId = id
            this.dialog = true
        },
        removeTodo() {
            this.$emit('remove-todo', this.removedTodoId)
        }
    }
};
</script>

