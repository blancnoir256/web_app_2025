<script setup lang="ts">
import { ref } from 'vue'

interface Todo {
    name: string
    isComplete: boolean
}

const todos = ref<Todo[]>([
    { name: '生命実験のレポートを書く', isComplete:true },
    { name: '全強になる', isComplete:false }
])
const newTodoName = ref('')
const newItemIsComplete = ref(false)

const addItem = () => {
    if (newTodoName.value == '') {
        return
    }
    todos.value.push({ name: newTodoName.value, isComplete: newItemIsComplete.value })
    newTodoName.value = ''
    newItemIsComplete.value = false
}
</script>

<template>
    <div>
        <h2 class="medatsu">ItemList</h2>
        <ul>
            <li v-for="item in todos" :key="item.name">
                <div :class="{ completed: item.isComplete }">やること: {{ item.name }}</div>
            </li>
        </ul>
        <div>
            <label>
                Todo
                <input v-model="newTodoName" type="text" />
            </label>
            <button @click="addItem">add</button>
        </div>
    </div>
</template>

<style>
.completed {
    text-decoration:line-through;
    color: gray;
}
.medatsu {
    color:yellowgreen
}
</style>