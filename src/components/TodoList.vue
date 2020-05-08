<template>
<div>
    <TodoItem v-for='todo of todos' :todo='todo' :key="todo.id"  @remove-todo='changeReconfirmDelete' />
    <div class="confirmBlock" v-if="removedTodoId">
        <p>Подтвердить удаление списка задач?</p>
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

<style scoped>
.reconfirm {
    border: 1px solid #00ff09;
    color: #00ff09;
    cursor: pointer;
    margin: 0px 10px;
}

.reconfirm:hover {
    background: #00ff09;
    color: #fff;
}

.cancel {
    border: 1px solid #ec5840;
    color: #ec5840;
    cursor: pointer;
    margin: 0px 10px;
}

.cancel:hover {
    background: #ec5840;
    color: #fff;
}
</style>
