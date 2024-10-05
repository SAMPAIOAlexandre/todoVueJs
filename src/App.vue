<script setup>
import { ref } from "vue";
const todos = ref([]);
const todo = ref("");
const addTodo = () => {
	todos.value.push({
		title: todo.value,
		completed: false,
		data: Date.now(),
	});
};
</script>

<template>
  <div>
    <h1>Hello bienvenue sur la todo list</h1>
    <form @submit.prevent="addTodo">
      <fieldset role="group">
    <input type="text"
    placeholder="Tâche à ajouter"
    v-model="todo">
    <button>Ajouter la tâche</button>
    </fieldset>
    </form>
    <div v-if="todos.length === 0"> Aucune tâche à faire </div>
    <div v-else>
      <ul>
        <li v-for="todo in todos"
        :key="todo.date">
        {{ todo.title }}
        </li>
      </ul>  
  
    </div>
  </div>

</template>


