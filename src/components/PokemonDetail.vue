<template>
  <div class="pokemon_detail">
    <div class="pokemon_detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <img :src="imgUrl + pokemon.id + '.png'" alt="" />
      </div>
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <div class="property">
          <div class="left">Base Experience</div>
          <div class="right">{{ pokemon.base_experience }} XP</div>
        </div>
        <div class="property">
          <div class="left">Height</div>
          <div class="right">{{ pokemon.height / 10 }} m</div>
        </div>
        <div class="property">
          <div class="left">Weight</div>
          <div class="right">{{ pokemon.weight }} kg</div>
        </div>
      </div>
    </div>
    <i v-else class="fas fa-spinner fa-spin"></i>
  </div>
</template>

<script>
export default {
  props: ["pokemonUrl", "imgUrl"],
  data: () => {
    return {
      show: false,
      pokemon: {},
    };
  },
  methods: {
    fetchPokemons() {
      let req = new Request(this.pokemonUrl);
      fetch(req)
        .then((resp) => {
          if (resp.status === 200) return resp.json();
        })
        .then((data) => {
          this.pokemon = data;
          this.show = true;
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
.pokemon_detail {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
  background: rgba($color: #000000, $alpha: 0.7);

  .pokemon_detail-view {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: relative;
    width: 100%;
    max-width: 510px;
    padding: 50px 0 0;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);

    .image {
      display: flex;
      justify-content: center;
      align-items: center;
      position: absolute;
      top: -60px;
      width: 120px;
      height: 120px;
      background-color: #333;
      border-radius: 50%;
      overflow: hidden;
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
    }

    h2 {
      text-transform: capitalize;
    }

    .data {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      flex-direction: column;
      width: 100%;
      margin-bottom: 40px;

      .property {
        width: 90%;
        max-width: 400px;
        border-bottom: 1px solid #ccc;
        margin-bottom: 10px;
        .left {
          float: left;
        }
        .right {
          float: right;
        }
      }
    }
  }
}
</style>
