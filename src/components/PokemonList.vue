<template>
  <div class="pokemon_list">
    <article v-for="(pokemon, index) in pokemons" :key="'poke' + index">
      <img :src="imgUrl + pokemon.id + '.png'" width="96" height="96" alt="" />
      <h3>{{ pokemon.name }}</h3>
    </article>
  </div>
</template>

<script>
export default {
  props: ["imgUrl", "apiCallUrl"],
  data: () => {
    return {
      pokemons: [],
      nextUrl: "",
    };
  },
  methods: {
    fetchPokemons() {
      let req = new Request(this.apiCallUrl);
      fetch(req)
        .then((resp) => {
          if (resp.status === 200) return resp.json();
        })
        .then((data) => {
          this.nextUrl = data.next;
          data.results.forEach((pokemon) => {
            pokemon.id = pokemon.url
              .split("/")
              .filter(function (part) {
                return !!part;
              })
              .pop();
            this.pokemons.push(pokemon);
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    this.fetchPokemons();
  },
};
</script>

<style lang="scss" scoped></style>
