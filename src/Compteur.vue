<!-- Exo pour prendre en main la base de Vue -->

<script setup>
import { ref } from "vue";
const count = ref(0);
const increment = () => {
	count.value++;
};
const decrement = () => {
	count.value--;
};
</script>

<template>
  <div>
    <h1>Hello</h1>
    <p>Compteur : {{ count }}</p>

    <!-- On peut utiliser la syntaxe v-on:click="increment" mais je trouve celle en dessous plus pratique -->
    <button @click="increment">Incrémenter</button>
    <button @click="decrement">Décrémenter</button>
    <div v-show="count >= 5">Bravo tu as appuyé 5 fois </div>
  </div>

</template>


