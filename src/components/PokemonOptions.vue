<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemonOption"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        {{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }}
      </li>
    </ul>
  </div>
</template>



<script>
export default {
  props: {
    pokemonOption: {
      type: Array,
      required: true,
    },
  },
  methods: {},
};
</script>




<style scoped>
ul {
  list-style-type: none;
}
li {
  background-color: white;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
  width: 250px;
}

li:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
  display: flex;
  justify-content: center;
}
</style>