<template>
  <div class="pokemon-card">
    <img :src="pokemonImage" alt="Pokemon" class="filtered-image"/>
    <!-- Otros elementos -->
  </div>
</template>

<script>
import axios from 'axios';
import PokemonCard from './components/PokemonCard.vue';

export default {
  name: 'App',
  components: {
    PokemonCard
  },
  data() {
    return {
      pokemons: [],
      discoveredCount: 0
    };
  },
  methods: {
    fetchPokemons() {
      axios.get('https://pokeapi.co/api/v2/pokemon?limit=20')
        .then(response => {
          const pokemonUrls = response.data.results.map(pokemon => pokemon.url);
          return Promise.all(pokemonUrls.map(url => axios.get(url)));
        })
        .then(responses => {
          this.pokemons = responses.map(response => response.data);
        });
    },
    incrementDiscoveredCount() {
      this.discoveredCount++;
    }
  },
  created() {
    this.fetchPokemons();
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 20px;
}
.pokemon-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
