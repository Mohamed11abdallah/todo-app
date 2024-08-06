
<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add New Todo</button>
  </form>
  <ul>
    <button @click="markAllDone" >Mark All Done</button>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
    <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h3>
    <button @click="removeTodo(index)" >Remove Todo</button>
  </li>

  </ul>

</template>

<script>
import { ref, reactive } from 'vue';

export default{
  setup(){
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo(){
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      })
      newTodo.value = '';
    }

    function toggleDone(todo){
      todo.done = !todo.done;
    }

    function removeTodo(index){
      todos.value.splice(index, 1);
    }

    function markAllDone(){
      todos.value.forEach((todo) => todo.done = true);
    }
    

    return {
      todos,
      newTodo,   
      addNewTodo,
      toggleDone,
      removeTodo, 
      markAllDone,
    };
  }
}
</script>


<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f5f5;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

h1 {
  color: #333;
  font-size: 2.5em;
  margin-bottom: 1.5em;
}

form {
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
  padding: 2em;
  width: 100%;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

label {
  margin-bottom: 0.5em;
  font-size: 1.1em;
  color: #666;
}

input {
  padding: 0.75em;
  font-size: 1.1em;
  border: 1px solid #ddd;
  border-radius: 6px;
  margin-bottom: 0.75em;
  transition: border-color 0.3s;
}

input:focus {
  border-color: #4a90e2;
  outline: none;
}

button {
  padding: 0.75em;
  font-size: 1.1em;
  color: #fff;
  background-color: #4a90e2;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-top: 0.5em;
}

button:hover {
  background-color: #357abd;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  background: #ffffff;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 1em;
  margin-bottom: 0.75em;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

h3 {
  margin: 0;
  color: #333;
  flex: 1;
  cursor: pointer;
}

.done {
  text-decoration: line-through;
  color: #888;
}

.todo button {
  background-color: #e32828;
  color: #fff;
  border-radius: 6px;
  padding: 0.5em 1em;
  font-size: 0.9em;
}

.todo button:hover {
  background-color: #e32828;
}
</style>
