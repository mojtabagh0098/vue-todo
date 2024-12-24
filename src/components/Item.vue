<script>
export default {
    props: ["todo"],
    data(){
        return {
            isEditting: false,
            editableText: this.todo.title
        }
    },
    methods: {
        removeTodo(todo)
        {
            this.$emit("remove-todo",todo);
        },
        editTodo(todo)
        {
            this.$emit("edit-todo",todo);
        },
        startEditing()
        {
            this.isEditting = true
        },
        saveEdit(todo)
        {
            this.isEditting = false
            // this.todo = {title: this.editableText, completed: this.todo.completed}
            this.$emit("edit-todo",{title: this.editableText, completed: false});
        }
    },
    watch: {
        'todo': {
            immediate: true,
            handler(newVal) {
                console.log(newVal);
                this.todo.title = newVal.title;
                
                
                // this.todo.title = newVal;
            },
        }
    }
}
</script>
<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <div class="form-check">
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" v-model="todo.completed" :checked="todo.completed">
        </div>
        <span class="me-auto fs-6 fw-bold" v-if="!isEditting" :class="{ 'text-decoration-line-through' :todo.completed}">{{ todo.title }}</span>
        <input class="form-control me-1" v-else type="text" name="add" v-model="editableText" />
        <button class="btn btn-success btn-sm me-1" v-if="isEditting" @click="saveEdit(todo)">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2-square" viewBox="0 0 16 16">
                <path d="M3 14.5A1.5 1.5 0 0 1 1.5 13V3A1.5 1.5 0 0 1 3 1.5h8a.5.5 0 0 1 0 1H3a.5.5 0 0 0-.5.5v10a.5.5 0 0 0 .5.5h10a.5.5 0 0 0 .5-.5V8a.5.5 0 0 1 1 0v5a1.5 1.5 0 0 1-1.5 1.5z"/>
                <path d="m8.354 10.354 7-7a.5.5 0 0 0-.708-.708L8 9.293 5.354 6.646a.5.5 0 1 0-.708.708l3 3a.5.5 0 0 0 .708 0"/>
            </svg>
        </button>
        <button class="btn btn-warning btn-sm me-1" v-else @click="startEditing()">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5z"/>
            </svg>
        </button>
        <button class="btn btn-danger btn-sm" @click="removeTodo(todo)">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
                <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0z"/>
                <path d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4zM2.5 3h11V2h-11z"/>
            </svg>
        </button>
    </li>
</template>