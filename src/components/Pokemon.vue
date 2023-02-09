<template>
  <div class="pokemon_container">
    <h1>The Pokemon's</h1>
    <PokemonList :imgUrl="imgUrl" :apiCallUrl="apiCallUrl" />
  </div>
</template>

<script>
import PokemonSearch from "./PokemonSearch.vue";
import PokemonList from "./PokemonList.vue";
import PokemonDetail from "./PokemonDetail.vue";

export default {
  data: () => {
    return {
      imgUrl:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon",
      apiCallUrl: "https://pokeapi.co/api/v2/pokemon/",
    };
  },
  components: {
    PokemonSearch,
    PokemonList,
    PokemonDetail,
  },
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css?family=Acme");
.pokemon_container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  background: radial-gradient(#0e161a, #000102);
  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}
</style>
