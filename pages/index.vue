<template>
  <div>
    <MainNav/>

    <main class="bg-gray-900 min-h-screen">
      <div class="container mx-auto px-4 sm:px-6 lg:px-8">
        <div class="py-8">
          <h1 class="text-4xl font-bold text-white text-center mb-8">All Pokemons</h1>
          <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
            <Card v-for="(pokemon, index) in pokemons" :key="pokemon.id" :pokemon="pokemon" :index="index"/>
          </div>
        </div>
      </div>

      <!--  load only 50 pokemons at once and load more on scroll -->
      <div class="flex justify-center">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mb-8" @click="loadMore">Load
          more
        </button>
      </div>


    </main>
  </div>
</template>

<script>
import Card from '@/components/Card.vue'
import MainNav from "@/components/MainNav.vue";

export default {
  name: 'Home',
  components: {
    Card,
    MainNav
  },
  data() {
    return {
      pokemons: [],
      nextUrl: 'https://pokeapi.co/api/v2/pokemon?limit=50'
    }
  },
  mounted() {
    this.loadMore()
  },
  methods: {
    loadMore() {
      fetch(this.nextUrl)
        .then(res => res.json())
        .then(data => {
          this.nextUrl = data.next
          data.results.forEach(pokemon => {
            fetch(pokemon.url)
              .then(res => res.json())
              .then(data => {
                this.pokemons.push(data)
              })
          })
        })
    }
  }
}
</script>



