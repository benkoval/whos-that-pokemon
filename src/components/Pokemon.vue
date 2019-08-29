<template>
    <main>
        <div>
            <h1>ayyylmao</h1>
            <button
            @click='getPokemon(getRandomInt())'>touch me</button>
        </div>
    </main>
</template>

<script>
import axios from "axios";

export default {
  name: 'HelloWorld',
  methods: { 
      getRandomInt() {
          return Math.floor(Math.random() * Math.floor(251))
      },
      getPokemon : async(id) => {
        const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        console.log(response.data.name)
      }
  }
}
</script>