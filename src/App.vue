<script setup>
import { ref } from "vue";
const todos = ref([
	{
		title: "tâche faites",
		completed: true,
		date: 4,
	},
	{
		title: "tâche pas faites",
		completed: false,
		date: 7,
	},
]);
const newTodo = ref("");
const isEditing = ref(null);
const addTodo = () => {
	todos.value.push({
		title: newTodo.value,
		completed: false,
		date: Date.now(),
	});
	/* Remet le champ à zéro après la validation */
	newTodo.value = "";
};
const orderedTodo = () => {
	return todos.value.toSorted((a, b) => (a.completed > b.completed ? 1 : 2));
};

const deleteTodo = (id) => {
	todos.value = todos.value.filter((todo) => todo.date !== id);
};

const editTodo = (id) => {
	isEditing.value = id;
};
const saveTodo = (id, newTitle) => {
	const task = todos.value.find((todo) => todo.date === id);
	if (task) {
		task.title = newTitle;
		isEditing.value = null;
	}
};
</script>

<template>
  <div>
    <h1>Bienvenue sur la todo list</h1>
    <form @submit.prevent="addTodo">
      <fieldset>
    <input type="text"
    placeholder="Tâche à ajouter"
    v-model="newTodo"> <!-- les données de l'input sont liées à ma variable "newTodo" -->
    <!-- Ici j'utilise 'disabled' si le champ ajouter une tâche est vide le button est bloqué -->
    <button :disabled="newTodo.length === 0">Ajouter la tâche</button>
    </fieldset>
    </form>
    <div v-if="todos.length === 0"> Aucune tâche à faire </div>
    <div v-else>
      <ul>
        <li v-for="todo in orderedTodo()" :key="todo.date">
          <div v-if="isEditing === todo.date">
            <input v-model="todo.title" />
            <button @click="saveTodo(todo.date, todo.title)">Sauvegarder</button>
          </div>
          <div v-else>
            {{ todo.title }}
            <label>
              <input type="checkbox" v-model="todo.completed" />
              <button @click="editTodo(todo.date)">Editer</button>
              <button @click="deleteTodo(todo.date)">Supprimer</button>
            </label>
          </div>
        </li>
      </ul>  
  
    </div>
  </div>

</template>

