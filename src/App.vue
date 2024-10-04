<script setup>
import { ref } from "vue";

const todos = ref([]);
</script>

<template>
  <div>
    <h1>Hello bienvenue sur la todo list</h1>

    <input type="text"
    placeholder="Tâche à ajouter">
    <button>Ajouter la tâche</button>
    <div v-if="todos.length === 0"> Aucune tâche à faire :) </div>
    <div>  
    <ul>
        <li>
          tâche 1
        </li>
        <li>
          tâche 2
        </li>
      </ul>
    </div>
  </div>

</template>


