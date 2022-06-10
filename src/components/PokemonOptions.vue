<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>
<style scoped>
ul {
  z-index: 100;
  position: absolute;
  top: 37%;
  list-style-type: none;
}
li {
  font-size: 20px;
  font-weight: bold;
  background-color: rgb(255, 213, 0);
  border-radius: 5px;
  border: 2px solid blue;
  color: rgb(0, 0, 0);
  cursor: pointer;
  margin-bottom: 10px;
  width: 250px;
  padding: 0.5em;
}

li:hover {
  background-color: rgba(255, 0, 0, 0.799);
  color: white;
}

.options-container {
  display: flex;
  justify-content: center;
}
</style>