<!-- Page to show a single pokemon and its details -->

<template>
  <div>
    <MainNav />
  <main class="bg-gray-900 min-h-screen py-8">

    <div class="flex justify-evenly mb-8">
      <div class="flex">
        <router-link :to="{ name: 'pokemon-id', params: { id: pokemon.id - 1 } }">
          <button v-if="pokemon.id > 1" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Previous
          </button>
        </router-link>
      </div>
      <div class="flex">
        <router-link :to="{ name: 'pokemon-id', params: { id: pokemon.id + 1 } }">
          <button v-if="pokemon.id < 1010" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Next
          </button>
        </router-link>
      </div>
    </div>


    <div class="container mx-auto px-4 sm:px-6 lg:px-8 ">
      <div class="border border-gray-700 py">


        <h2 class="text-4xl  text-center font-semibold text-gray-100 capitalize mt-8">{{ pokemon.name }}</h2>
        <h5 class="text-2xl  text-center font-semibold text-gray-100 capitalize">#{{ pokemon.id }}</h5>

        <!--Sprites-->
        <div class="flex justify-center">
          <img :src="pokemon.sprites && pokemon.sprites.front_default" :alt="pokemon.name" class="w-32 h-32"/>
          <img :src="pokemon.sprites && pokemon.sprites.back_default" :alt="pokemon.name" class="w-32 h-32"/>
        </div>
        <p class="text-center text-gray-100">Default sprites</p>


      </div>


      <!--Types-->
      <div class="border border-gray-700 py-8">
        <h2 class="text-4xl  text-center font-semibold text-gray-100 capitalize">Types</h2>
        <div class="flex justify-center">
          <div v-for="type in pokemon.types" :key="type.type.name"
               class="bg-gray-700 rounded-full px-4 py-2 m-4 capitalize">
            <p class="text-gray-100">{{ type.type.name }}</p>
          </div>
        </div>
      </div>

      <!--Abilities-->
      <div class="border border-gray-700 py-8">
        <h2 class="text-4xl  text-center font-semibold text-gray-100 capitalize">Abilities</h2>
        <div class="flex justify-center">
          <div v-for="ability in pokemon.abilities" :key="ability.ability.name"
               class="bg-gray-700 rounded-full px-4 py-2 m-4 capitalize">
            <p class="text-gray-100">{{ ability.ability.name }}</p>
          </div>
        </div>
      </div>

      <!--Stats in a table-->
      <div class="border border-gray-700 py-8">
        <h2 class="text-4xl  text-center font-semibold text-gray-100 capitalize">Stats</h2>
        <table class="table-auto w-8/12 mx-auto">
          <thead>
          <tr>
            <th class="px-4 py-2 text-gray-100">Name</th>
            <th class="px-4 py-2 text-gray-100">Base stat</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="stat in pokemon.stats" :key="stat.stat.name">
            <td class="border px-4 py-2 text-gray-100 capitalize">{{ stat.stat.name }}</td>
            <td class="border px-4 py-2 text-gray-100 text-center">{{ stat.base_stat }}</td>
          </tr>
          </tbody>
        </table>
      </div>


      <!--Moves in a table with how they are learned-->
      <div class="border border-gray-700 py-8">
        <h2 class="text-4xl  text-center font-semibold text-gray-100 capitalize">Moves</h2>
        <table class="table-auto w-8/12 mx-auto">
          <thead>
          <tr>
            <th class="px-4 py-2 text-gray-100">Name</th>
            <th class="px-4 py-2 text-gray-100">Learn method</th>
            <th class="px-4 py-2 text-gray-100">Level</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="move in pokemon.moves" :key="move.move.name">
            <td class="border px-4 py-2 text-gray-100 capitalize">{{ move.move.name }}</td>
            <td class="border px-4 py-2 text-gray-100 capitalize">{{ move.version_group_details[0].move_learn_method.name }}</td>
            <td class="border px-4 py-2 text-gray-100 text-center">{{ move.version_group_details[0].level_learned_at }}</td>
          </tr>
          </tbody>
        </table>
      </div>

      <!--Back to home-->
      <div class="flex justify-center mt-8">
        <router-link to="/">
          <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Back to home
          </button>
        </router-link>

        </div>

    </div>





  </main>
  </div>
</template>

<script>
import MainNav from "@/components/MainNav.vue";

export default {
  components: {
    MainNav
  },
  name: 'Pokemon',
  data() {
    return {
      pokemon: {}
    }
  },
  mounted() {
    fetch(`https://pokeapi.co/api/v2/pokemon/${this.$route.params.id}`)
      .then(response => response.json())
      .then(data => {
        this.pokemon = data
      })
  }
}
</script>


