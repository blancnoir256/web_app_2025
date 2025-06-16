<script setup lang="ts">
import { ref } from 'vue'

interface Todo {
    name: string
    isComplete: boolean
}

const todos = ref<Todo[]>([
    { name: '生命実験のレポートを書く', isComplete: true },
    { name: '全強になる', isComplete: false }
])
const newTodoName = ref('')
const newTodoIsComplete = ref(false)

const addtodo = () => {
    if (newTodoName.value === '') {
        return
    }
    todos.value.push({ name: newTodoName.value, isComplete: newTodoIsComplete.value })
    newTodoName.value = ''
    newTodoIsComplete.value = false
}
</script>

<template>
    <div>
        <h2 class="medatsu">TodoList</h2>
        <h3>completed list</h3>
        <ul>
            <li v-for="todo in todos.filter(todo => todo.isComplete)" :key="todo.name">
                <div :class="{ completed: todo.isComplete }">やること: {{ todo.name }}
                    <input type="checkbox" v-model="todo.isComplete">
                </div>
            </li>
            <div v-if="todos.filter(todo => todo.isComplete).length == 0">
                特になし
            </div>
        </ul>
        <h3>uncompleted list</h3>
        <ul>
            <li v-for="todo in todos.filter(todo => !todo.isComplete)" :key="todo.name">
                <div :class="{ completed: todo.isComplete }">やること: {{ todo.name }}
                    <input type="checkbox" v-model="todo.isComplete">
                </div>
            </li>
            <div v-if="todos.filter(todo => !todo.isComplete).length == 0">
                特になし
            </div>
        </ul>
        <div>
            <label>
                Todo
                <input v-model="newTodoName" type="text" />
            </label>
            <button @click="addtodo">add</button>
        </div>
    </div>
</template>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}

.medatsu {
    color: yellowgreen
}
</style>