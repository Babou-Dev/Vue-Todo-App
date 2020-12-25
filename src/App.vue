<template>
  <h1>Vue 3 Todo App by BabouDeb</h1>
  <form @submit.prevent="addNewTodo">
      <label>New Todo Here =></label>
      <input v-model="newTodo" name="newTodo">
      <button>Add new Todo</button>
  </form>
  <div class="buttondiv">
    <button @click="markAllDone">Mark All Done</button>
    <button @click="removeAllTodos">Remove All</button>
  </div>
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
      todos.value.forEach((todo) => todo.done = true);
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
* {
  background-color: rgb(46, 46, 46);
}

#app {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: yellow;
  margin-top: 60px;
}

h1 {
  padding: 10px 25px;
  font-size: 50px;
}

.buttondiv {
  margin: auto;
  width: 50%;
  padding: 10px;
}

button {
  background-color: white;
  border: none;
  position: relative;
  padding: 10px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}

form label {
  padding: 12px 20px;
  font-size: 20px;
}

form button {
  margin: 12px 20px;
  padding: 15px 20px;
  font-size: 16px;
}

form input {
  width: 75%;
  background-color: grey;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  font-size: 16px;
}

.done {
  text-decoration: line-through;
  color: green;
}

.todo {
  cursor: pointer;
  list-style: none;
}
</style>
