<template>
  <main class="bg-gray-900 min-h-screen">
    <div class="container mx-auto px-4 sm:px-6 lg:px-8">
      <div class="py-8">
        <h1 class="text-4xl font-bold text-white text-center mb-8">Pokedex</h1>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
          <Card v-for="(poke, index) in pokemon" :poke="poke" :index="index" :key="index" />
        </div>
      </div>
    </div>

    <!--  load only 50 pokemons at once and load more on scroll -->
    <div class="flex justify-center">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mb-8" @click="loadMore">Load more</button>
    </div>


  </main>
</template>

<script>
import Card from '@/components/Card.vue'
 export default {
   name: 'Home',
   components: {
     Card
   },
   data() {
     return {
       pokemon: [],
       nextUrl: 'https://pokeapi.co/api/v2/pokemon?limit=50'
     }
   },
   mounted() {
     this.loadMore()
   },
   methods: {
     loadMore() {
       fetch(this.nextUrl)
         .then(response => response.json())
         .then(data => {
           this.nextUrl = data.next
           data.results.forEach(pokemon => {
             fetch(pokemon.url)
               .then(response => response.json())
               .then(data => {
                 this.pokemon.push(data)
               })
           })
         })
     }
   }
 }
</script>


