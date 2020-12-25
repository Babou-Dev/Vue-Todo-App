<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
      <label>New Todo</label>
      <input v-model="newTodo" name="newTodo">
      <button>Add new Todo</button>
  </form>
  <button @click="markAllDone">Mark All Done</button>
  <button @click="removeeAllTodos">Remove All</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)" >{{todo.content}}</h3>
      <button @click="removeTodo(index)">Remove Todo</button>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');

    const todos = ref([]);

    function addNewTodo() {
      todos.value.push ({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDown(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true)
    }

    function removeAllTodos() {
      todos.value.length = 0;
    }

    return {
      newTodo,
      addNewTodo,
      todos,
      toggleDown,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}

.todo {
  cursor: pointer;
}
</style>
