<template>
  <Layout>
    <form @submit.prevent="fetchPokemon(searchTerm)">
      <input type="text" v-model="searchTerm" placeholder="pikachu" />
      <button type="submit">Search</button>
    </form>

    <div class="pokemon-card--container">
      <h2 class="pokemon-card--title">{{pokemon.name}}</h2>
      <img v-if="pokemon.imageUrl" :src="pokemon.imageUrl" />
    </div>
  </Layout>
</template>

<script>
export default {
  data() {
    return {
      url: 'https://pokeapi.co/api/v2',
      searchTerm: '',
      pokemon: {
        imageUrl: '',
        name: ''
      }
    }
  },
  methods: {
    async fetchPokemon(searchTerm) {
      try {
        const resp = await fetch(`${this.url}/pokemon/${searchTerm}`)
        const data = await resp.json()
        console.log(data)

        this.pokemon.name = data.name
        this.pokemon.imageUrl = data.sprites.front_default
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style>
.pokemon-card--container {
}
.pokemon-card--title {
}
</style>