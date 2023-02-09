<template>
  <div class="pokemon_list"></div>
</template>

<script>
export default {
  props: [imgUrl, apiCallUrl],
  data: () => {
    return {
      pokemons: [],
    };
  },
  mathods: {
    fetchPokemons() {
        let req = new Request(this.apiCallUrl);
        fetch(req)
        .then((res) => {
            if(res.status = 200) 
            return res.json();
        })
    }
  }
};
</script>

<style></style>
