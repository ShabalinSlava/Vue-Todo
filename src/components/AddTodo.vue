<template>
<div>
    <button class='create-todo create-todo-margin' v-on:click='openForm' v-show='!isCreating'>Создать</button>
    <!-- При клике на конопку создать. Срабатывает v-show и появляется блок для создания дел -->
    <div v-show='isCreating'>
        <!-- При submit страница перезагружается. Prevent сбрасывает это состояние. Так как нам нужно, что бы только на кнопку с type submit было сохранение и закрытие блока. -->
        <form class='form' @submit.prevent='onSubmit'>
            <div class='field'>
                <label>Заголовок:</label>
                <input v-model="task.title" type='text' ref='title' defaultValue="">
            </div>
            <div class='field' v-for="projects of task.projects" :key="projects.id">
                <label>Задача:</label>
                <input v-model="projects.task" type='text' ref='projects' defaultValue="">
            </div>

            <div class='buttons'>
                <button type="button" class='create-todo' v-on:click="createProject()">
                    Добавить задачу
                </button>
                <button type="submit" class='create-todo'>
                    Сохранить
                </button>
                <button class='cancel-todo' v-on:click="closeForm" type="button">
                    Отмена
                </button>
            </div>
        </form>
    </div>
</div>
</template>

<script>
export default {
    // Параметры, которые будут входить при создании задачи
    data() {
        return {
            task: {
                title: '',
                projects: [{
                    id: 1,
                    task: '',
                    completed: false
                }],
            },
            isCreating: false,
        };
    },
    methods: {
        // Открыть блок для создания
        openForm() {
            this.isCreating = true;
        },
        // Закрыть блок для создания
        closeForm() {
            this.isCreating = false;
        },
        // Значение, которое должны быть добавлено при создании нового пункта
        createProject() {
            const id = this.task.projects.length + 1
            this.task.projects.push({
                id,
                task: '',
                completed: false
            })
        },
        onSubmit() {
            const newTodo = this.task
            this.$emit('add-todo', newTodo);
            this.task = {
                    title: '',
                    projects: [{
                        id: 1,
                        task: '',
                        completed: false
                    }],
                },
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
    border: 1px solid #2199e8;
    color: #2199e8;
    cursor: pointer;
}

.create-todo-margin {
    margin-bottom: 10px;
}

.create-todo:hover {
    background: #2199e8;
    color: #fff;
}

input {
    margin-left: 10px;
}

.buttons {
    max-width: 300px;
    display: flex;
    justify-content: space-between;
    margin: auto
}

.cancel-todo {
    border: 1px solid #ec5840;
    color: #ec5840;
    cursor: pointer;
}

.cancel-todo:hover {
    background: #ec5840;
    color: #fff;
}
</style>
