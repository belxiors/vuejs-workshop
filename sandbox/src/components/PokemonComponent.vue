<template>
  <h2>{{ pokemon.name }}</h2>
  <button @click="handleMoreInfoClick">Find out more about {{ pokemon.name.toUpperCase() }}</button>
  <ul v-if="pokemonInfo">
    <li :key="index" v-for="(ability, index) in pokemonInfo.abilities">
      {{ ability.ability.name }}
    </li>
  </ul>
</template>
<script setup>
import { ref } from 'vue'
const props = defineProps(['pokemon'])
const pokemonInfo = ref(null)

async function handleMoreInfoClick() {
  const info = await fetch(props.pokemon.url).then((response) => response.json())
  pokemonInfo.value = info
}
</script>
