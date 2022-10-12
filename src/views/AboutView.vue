<template>
  <div class="about">
    <div class="pokemon" v-if="pokemon">
      <h3 class="pokemon_name">
        {{pokemon.name}}
      </h3>
      <div class="pokemon_card">
        <img class="pokemon_image" :src="pokemon.sprites.front_shiny" alt="">
        <img class="pokemon_image" :src="pokemon.sprites.back_shiny" alt="">
      </div>
      <p class="type_title">Types</p>
      <div v-for="(type, index) in pokemon.types" :key="index">
        <p class="type_name">{{type.type.name}}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import {useRoute} from "vue-router"
import {reactive, onMounted, toRefs} from "vue"
const route = useRoute();
const state = reactive({
  pokemon: null
})
const { pokemon } = toRefs(state)

async function fetchPokemon() {
  const result = await fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}`);
  const foundPokemon = await result.json();

  console.log(foundPokemon);
  state.pokemon = foundPokemon;
}

onMounted(fetchPokemon);
</script>

<style scoped>
  .pokemon{
    min-width: 24rem;
    width: 25%;
    margin: auto;
    padding: 20px 0;
    background-color: rgba(244, 196, 244, 0.319);
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    display: flex;
    flex-direction: column;
    align-items: center;
    outline: 2px solid rgb(14, 34, 119) ;
    border-radius: 40px;
  }
  .pokemon_name{
    font-size: 1.5rem;
    line-height: 2rem;
    color: rgb(30, 58, 138);
    text-transform: uppercase;
    padding: 0;
    margin: 0;
  }

  .pokemon_card{
    display: flex;
    justify-content: center;
  }

  .pokemon_image{
    width: 12rem
  }

  .type_title{
    font-size: 1.5rem;
    margin-top: 0;
    color: rgb(255, 187, 0);
  }

  .type_name{
    font-size: 1.2rem;
    color: rgb(30, 58, 138);
    margin: 0;
    padding: 5px 0;
  }
</style>
