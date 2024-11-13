<template>
  <h1>Hello World!</h1>
  <div id="app">
    <button @click="fetchPokemons">Get my pokemons</button>
    <div :key="pokemon.name" v-for="pokemon in pokemonList">
      <PokemonComponent :pokemon="pokemon" />
    </div>
    <hr />
    <h1>{{ count }}</h1>
    <button v-on:click="incremenetCount">Increment Count</button>
    <div>
      <label>Incrememt by:</label>
      <input type="number" v-bind:value="incrementAmount" v-on:input="changeIncremenetAmount" />
    </div>
    <hr />
    <p v-if="message.length % 2 === 0">Even: {{ message }}</p>
    <p v-else>Odd: {{ message }}</p>
    <ul>
      <li v-for="number in listOfNumbers" :key="number.id">{{ number.num }}</li>
    </ul>
  </div>
</template>
<script setup>
import { ref } from 'vue'
import PokemonComponent from './components/PokemonComponent.vue'
const pokemonList = ref([])
const count = ref(0)
const incrementAmount = ref(8)
const message = 'Hello from vue side!'
const listOfNumbers = [
  { num: 1, id: 'a30be468-4c9b-47c1-9371-3bf3d44d42de' },
  { num: 2, id: '6d3b95b4-5893-4e9e-9749-9d789af458ab' },
  { num: 3, id: 'e2e79f5c-d1bb-435a-bc5a-473bdd105fb2' },
  { num: 4, id: '6c1910c2-a4fe-4ce4-8201-043c887847d2' },
  { num: 5, id: '860a43d6-94b2-4351-aa64-ab227b8ee0a9' }
]

function incremenetCount() {
  count.value += incrementAmount.value
}

function changeIncremenetAmount(event) {
  incrementAmount.value = Number(event.target.value)
}

async function fetchPokemons() {
  const pokemons = await fetch('https://pokeapi.co/api/v2/pokemon').then((response) =>
    response.json()
  )
  pokemonList.value = pokemons.results
}
</script>
