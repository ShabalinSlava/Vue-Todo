<template>
<div>
    <TodoItem v-for='(todo, i) of todos' :todo='todo' :key="todo.id" :index='i' @remove-todo='changeReconfirmDelete' />
    <div class="confirmBlock" v-if="removedTodoId">
        Подтвердить удаление
        <button class="reconfirm" @click="removeTodo">Подтвердить</button>
        <button class="cancel" @click="removedTodoId = null; confirmBlock = !confirmBlock">Отмена</button>
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
            confirmBlock: false
        }
    },
    methods: {
        changeReconfirmDelete(id) {
            this.removedTodoId = id
            this.confirmBlock = true
        },
        removeTodo() {
            this.$emit('remove-todo', this.removedTodoId)
        }
    }
};
</script>
