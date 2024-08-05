<template>
  <div class="pokemon-card">
    <img :src="pokemonImage" alt="Pokemon" class="filtered-image"/>
    <!-- Otros elementos -->
  </div>
</template>

<script>
export default {
  props: {
    pokemonImage: String,
    // Otras props
  },
  // Otro código de script
}
</script>

<style scoped>
.filtered-image {
  filter: blur(5px); /* Puedes ajustar el valor de desenfoque según sea necesario */
}
</style>
