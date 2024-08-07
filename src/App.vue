<template>
  <div class="container">
    <h1>Vue 3 Todo App</h1>
    <form @submit.prevent="addNewTodo" class="todo-form">
      <label for="newTodo">New Todo</label>
      <input v-model="newTodo" type="text" id="newTodo" placeholder="What needs to be done?">
      <button type="submit">Add New Todo</button>
    </form>
    <div class="buttons">
      <button @click="markAllDone" class="mark-done-btn">Mark All Done</button>
      <button @click="removeAllTodos" class="remove-all-btn">Remove All</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="todo.id" :class="{ done: todo.done }" class="todo">
        <h3 @click="toggleDone(todo)">{{ todo.content }}</h3>
        <button @click="removeTodo(index)" class="remove-todo-btn">Remove Todo</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('');
const todos = ref([]);

function addNewTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({
      id: Date.now(),
      done: false,
      content: newTodo.value,
    });
    newTodo.value = '';
  }
}

function markAllDone() {
  todos.value.forEach((todo) => (todo.done = true));
}

function toggleDone(todo) {
  todo.done = !todo.done;
}

function removeTodo(index) {
  todos.value.splice(index, 1);
}

function removeAllTodos() {
  todos.value = [];
}
</script>

<style scoped>
.container {
  width: 500px;
  /* margin: 50px auto; */
  padding: 20px;
  background: #f9f9f9;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  /* text-align: center; */
  margin-left: 50%;
}

h1 {
  color: #333;
  font-size: 24px;
  font-weight: 500;
  margin-bottom: 20px;
  text-align: center;
}

.todo-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-bottom: 20px;
}

.todo-form label {
  font-size: 20px;
  color: #555;
  font-weight: 500;
}

.todo-form input {
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ddd;
  border-radius: 10px;
}

.todo-form button {
  padding: 10px;
  font-size: 14px;
  color: #fff;
  background: #007bff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.buttons {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}

.mark-done-btn, .remove-all-btn {
  padding: 10px;
  font-size: 14px;
  color: #fff;
  background: #28a745;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.remove-all-btn {
  background: #dc3545;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-bottom: 10px;
  cursor: pointer;
}

.todo h3 {
  margin: 0;
  font-size: 20px;
}

.todo.done h3 {
  text-decoration: line-through;
  color: forestgreen;
  
}

.remove-todo-btn {
  padding: 5px 10px;
  font-size: 12px;
  color: #fff;
  background: #dc3545;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
