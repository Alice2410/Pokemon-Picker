<script  setup>
import { computed } from '@vue/reactivity';
import { reactive, onMounted, toRefs } from 'vue';

const state = reactive({
  pokemons: [],
  urlIdLookup: {},
  text: "",
  filteredPokemon:computed(() => updatePokemon())
});

const { urlIdLookup, text, filteredPokemon } = toRefs(state)

async function fetchPokemons() {
  const result = await fetch('https://pokeapi.co/api/v2/pokemon?offset=0');
  const pokemonRes = await result.json();

  state.pokemons = pokemonRes.results;
  state.urlIdLookup = pokemonRes.results.reduce((acc, currentValue, index) => 
  acc = {...acc, [currentValue.name]:index+1}
  ,{})
}

function updatePokemon() {
  if(!state.text) {
    return []
  }
  

  return state.pokemons.filter((pokemon) => {
    return pokemon.name.includes(state.text)
  })
}

onMounted(fetchPokemons);

</script>

<template>
  <div class="pokemon-input-container">
    <input class="pokemon-input" type="text" placeholder="Enter Pokemon here" v-model="text"> 
  </div>

  <div class="pokemons-container">
    <div class="pokemons-name" v-for="(pokemon, index) in filteredPokemon" :key="index">
      <router-link class="pokemons-link" :to="`/about/${urlIdLookup[pokemon.name]}`">
        {{pokemon.name}}
      </router-link>
    </div>
  </div>
</template>

<style scoped>
  .pokemon-input-container{
    width: 100%;
    display: flex;
    justify-content: center; 
  }

  .pokemon-input{
    margin-top: 2.5rem;
    padding: 0.5rem;
    border: solid rgb(14, 34, 119) 2px;
    border-radius: 5px;
  }

  .pokemons-container{
    margin-top: 2.5rem;
    padding: 1rem;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }

  .pokemons-name{
    margin-left: 1rem;
    font-size: 1rem;
    line-height: 1.5rem;
    color: rgb(120, 141, 194);
  }

  .pokemons-link{
    text-decoration: none;
  }
</style>

