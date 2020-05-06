<template>
<div>
    <div class='content-todo' v-show='!isEditing'>
        <h2>{{ todo.title }}</h2>
        <ul>
            <li>
                <span v-bind:class='{done: todo.completed}'>
                    <input type='checkbox' v-on:change='todo.completed = !todo.completed' />
                    <strong>{{ index + 1 }}</strong>
                    {{ todo.project }}
                </span>
            </li>
        </ul>
        <div class='buttons'>
            <button class='delete-todo' v-on:click='$emit("remove-todo", todo.id)'>Удалить</button>
            <button class='change-todo' v-on:click='showForm'>Изменить</button>
        </div>
    </div>
    <div class='content-todo content-change' v-show='isEditing'>
        <div class='field'>
            <label>Заголовок:</label>
            <input type='text' v-model="todo.title">
        </div>
        <div class='field'>
            <label>Задача:</label>
            <input type='text' v-model="todo.project">
        </div>
        <button class='change-todo' v-on:click='hideForm'>Закрыть</button>
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
        index: Number
    },
    data() {
        return {
            isEditing: false,
        }
    },
    methods: {
        showForm() {
            this.isEditing = true;
        },
        hideForm() {
            this.isEditing = false;
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
