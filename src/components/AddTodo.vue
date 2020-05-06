<template>
<div>
    <button class='create-todo' v-on:click='openForm' v-show='!isCreating'>Создать</button>
    <div v-show='isCreating'>
        <form class='form' @submit.prevent='onSubmit'>
            <div class='field'>
                <label>Заголовок:</label>
                <input v-model="title" type='text' ref='title' defaultValue="">
            </div>
            <div class='field'>
                <label>Задачи:</label>
                <input v-model="project" type='text' ref='project' defaultValue="">
            </div>
            <div class='buttons'>
                <button class='create-todo' v-on:click="onSubmit()">
                    Создать
                </button>
                <button class='delete-todo' v-on:click="closeForm">
                    Отмена
                </button>
            </div>
        </form>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            title: '',
            project: '',
            isCreating: false,
        };
    },
    methods: {
        openForm() {
            this.isCreating = true;
        },
        closeForm() {
            this.isCreating = false;
        },
        onSubmit() {
            if (this.title.trim() && this.project.trim()) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    project: this.project,
                    completed: false,
                }
                this.$emit('add-todo', newTodo);
                this.title = ''
                this.project = ''
            }
            this.isCreating = false;
        },
    },
};
</script>

<style scoped>
.form {
    max-width: 600px;
    margin: auto;
    border: 1px solid #ccc;
    margin-bottom: 30px;
    padding: 20px 0px;
    border-radius: 10px;
}

.field {
    margin-bottom: 10px;
}

.create-todo {
    border: 1px solid #3700ff;
    color: #3700ff;
    cursor: pointer;
    margin-bottom: 10px;
}

.create-todo:hover {
    background: #3700ff;
    color: #fff;
}


input {
    margin-left: 10px;
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
</style>
