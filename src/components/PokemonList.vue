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

<style lang="scss" scoped>
.pokemon_list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;

  article {
    height: 150px;
    background-color: #efefef;
    text-align: center;
    text-transform: capitalize;
    border-radius: 5px;
    cursor: pointer;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
    h3 {
      margin: 0;
    }
  }
}
</style>
