<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else>
    <h1>¿Cuál es este Pokémon?</h1>
    <PokemonPicture
      :pokemonId="pokemon.id"
      :showPokemon="showPokemon"
    ></PokemonPicture>

    <PokemonOptions
      :pokemons="pokemonArr"
      @selection="checkAnswer"
      v-show="showOption"
    />

    <template v-if="showAnswer">
      <h2 class="fade-in respuesta">{{ message }}</h2>

      <boton-leo @click-boton="newGame" leyenda="Nuevo juego"></boton-leo>
    </template>
  </div>
</template>
<script>
import PokemonOptions from "@/components/PokemonOptions.vue";
import PokemonPicture from "@/components/PokemonPicture.vue";
import getPokemonOptions from "@/helpers/getPokemonOptions.js";
import BotonLeo from "@/components/BotonLeo.vue";

export default {
  components: {
    PokemonPicture,
    PokemonOptions,
    "boton-leo": BotonLeo,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
      showOption: true,
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);

      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;
      if (selectedId === this.pokemon.id) {
        this.showOption = false;
        this.message = `Correcto, ${this.pokemon.name}"`;
      } else {
        this.message = `Oops, era ${this.pokemon.name}`;
        this.showOption = false;
      }
    },
    newGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.message = "";
      this.showOption = true;
      this.mixPokemonArray();
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>
<style>
h1 {
  font-size: 4em;
  color: rgb(255, 213, 0);
  text-shadow: -5px 0 blue, 0 6px blue, 5px 0 blue, 0 -6px blue;
  font-weight: bold;
  text-align: center;
  margin-top: 100px;
}
</style>