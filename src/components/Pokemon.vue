<template>
  <div class="pokemon_container">
    <img :src="require(`@/assets/pokemonImg.png`)" />
    <PokemonSearch :apiCallUrl="apiCallUrl" @setPokemonUrl="setPokemonUrl" />
    <PokemonList
      :imgUrl="imgUrl"
      :apiCallUrl="apiCallUrl"
      @setPokemonUrl="setPokemonUrl"
    />
    <PokemonDetail
      v-if="showDetail"
      :pokemonUrl="pokemonUrl"
      :imgUrl="imgUrl"
      @closeDetail="closeDetail"
    />
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
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      apiCallUrl: "https://pokeapi.co/api/v2/pokemon/",
      pokemonUrl: "",
      showDetail: false,
    };
  },
  components: {
    PokemonSearch,
    PokemonList,
    PokemonDetail,
  },
  methods: {
    setPokemonUrl(url) {
      this.pokemonUrl = url;
      this.showDetail = true;
    },
    closeDetail() {
      this.pokemonUrl = "";
      this.showDetail = false;
    },
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
  background: radial-gradient(#432626, #cc393b);
  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

img {
  margin-bottom: 30px;
}

h1 {
  color: #efefef;
}
</style>
