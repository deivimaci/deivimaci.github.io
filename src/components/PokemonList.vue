<template>
  <div class="list">
    <pokemon-card
      v-for="(pokemon, i) in advancedPokemonInfo"
      :key="i"
      :name="pokemon.data.name"
      :imageSrc="pokemon.data.sprites.front_default"
      :favourite="favourite"
      @setFavourite="handleFavourite"
    />
  </div>
</template>

<script>
import axios from "axios";
import PokemonCard from "@/components/PokemonCard.vue";

export default {
  components: { PokemonCard },
  data() {
    return {
      basicPokemonInfo: [],
      advancedPokemonInfo: [],
      favourite: "",
    };
  },
  methods: {
    // fetching pokemon data
    getPokemonData() {
      const url = "https://pokeapi.co/api/v2/pokemon?limit=10";
      axios
        .get(url)
        .then((response) => {
          // assigning fetched data to a variable
          this.basicPokemonInfo = response.data.results;
          // logging 10 pokemons
          console.table(response.data.results);
          // mapping through basic pokemon info and fetching advanced pokemon info
          const promises = this.basicPokemonInfo.map((res) => {
            return axios.get(res.url);
          });
          // assinging advanced pokemon info when all promises are resolved
          Promise.all(promises).then((response) => {
            this.advancedPokemonInfo = response;
          });
        })
        // catching if error occurs
        .catch((e) => console.log(e));
    },
    // Set favourite pokemon
    handleFavourite(name) {
      this.favourite = this.favourite !== name ? name : "";
    },
  },
  created() {
    // calling method to get pokemon data
    this.getPokemonData();
  },
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
  grid-gap: 20px;
  justify-items: stretch;
  max-width: 800px;
  margin: 0 auto;
}
</style>
