<script setup>
import { ref } from "vue";
const todos = ref([
	{
		title: "tâche faites",
		completed: true,
		data: 4,
	},
	{
		title: "tâche pas faites",
		completed: false,
		data: 7,
	},
]);
const newTodo = ref("");
const addTodo = () => {
	todos.value.push({
		title: newTodo.value,
		completed: false,
		data: Date.now(),
	});
	/* Remet le champ à zéro après la validation */
	newTodo.value = "";
};
const orderedTodo = () => {
	return todos.value.toSorted((a, b) => (a.completed > b.completed ? 1 : 2));
};

const deleteTodo = (id) => {
	todos.value = todos.value.filter((todo) => todo.data !== id);
};
</script>

<template>
  <div>
    <h1>Hello bienvenue sur la todo list</h1>
    <form @submit.prevent="addTodo">
      <fieldset role="group">
    <input type="text"
    placeholder="Tâche à ajouter"
    v-model="newTodo">
    <!-- Ici j'utilise disabled si le champ ajouter une tâche est video le button est bloqué -->
    <button :disabled="newTodo.length === 0">Ajouter la tâche</button>
    </fieldset>
    </form>
    <div v-if="todos.length === 0"> Aucune tâche à faire </div>
    <div v-else>
      <ul>
        <li v-for="todo in orderedTodo()"
        :key="todo.date">
        {{ todo.title }}
        <label>
          <input type="checkbox" v-model="todo.completed">
          
          <button @click="deleteTodo(todo.data)">Supprimer</button>
        </label>
        </li>
      </ul>  
  
    </div>
  </div>

</template>


