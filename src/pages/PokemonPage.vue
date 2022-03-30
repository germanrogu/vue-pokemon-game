<template>
  <h1 v-if="!pokemon">Espere por favor ...</h1>
  <div v-else>
    <h1>¿Quién es este pokémon?</h1>

    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />

    <PokemonOptions
      :pokemonOption="pokemonArr"
      @selection="checkAnswer($event)"
    />

  <template v-if="showAnswer" class="fade-in">
    <h2 >{{ message }}</h2>
      <button @click="newGame">Nuevo juego</button>
  </template>
   
    
  </div>
</template>




<script>
import PokemonPicture from "../components/PokemonPicture.vue";
import PokemonOptions from "../components/PokemonOptions.vue";

import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  name: "PokemonPage",
  components: {
    PokemonPicture,
    PokemonOptions,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(pokemonId) {
      this.showAnswer = true;
      if (pokemonId === this.pokemon.id) {
        this.showPokemon = true;
        this.message = `¡Correcto! El pokemon es ${this.pokemon.name}`;
      } else {
        this.message = "Oops incorrecto!";
      }
    },
    newGame() {
      this.showAnswer = false;
      this.showPokemon = false;
      this.pokemonArr = [];
      this.message = "";
      this.pokemon = null;
      this.mixPokemonArray();
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>

