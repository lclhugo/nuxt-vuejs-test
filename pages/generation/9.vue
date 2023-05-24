<!-- Pokemon generation 1 -->
<template>
    <main class="bg-gray-900 min-h-screen">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="py-8">
                <h1 class="text-4xl font-bold text-white text-center mb-8">Generation 9</h1>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
                    <Card v-for="(pokemon, index) in pokemons" :key="pokemon.id" :pokemon="pokemon" :index="index" />
                </div>
            </div>
        </div>
    </main>
</template>
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
            pokemons: [],
            nextUrl: 'https://pokeapi.co/api/v2/pokemon?offset=905&limit=105'
        }
    },
    mounted() {
        this.loadeverything()
    },
    methods: {
        loadeverything() {
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

    


       