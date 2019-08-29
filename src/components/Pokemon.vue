<template>
    <main>
        <div>
            <h1>ayyylmao</h1>
            <button
            @click='getPokemon(getRandomInt())'>touch me</button>
            <img :src="frontSprite"/>
        </div>
    </main>
</template>

<script>
import axios from "axios";

export default {
  name: 'Pokemon',
  data: async () => {
      return {
          frontSprite: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/173.png"
      }
  },
  async mounted() {
    //   let frontSprite = ''
      await this.getPokemon(this.getRandomInt());
  },
  methods: { 
      getRandomInt() {
          console.log('hi', this.frontSprite)
          return Math.floor(Math.random() * Math.floor(251))
      },
      getPokemon : async(id) => {
        // console.log('async', this.frontSprite)
        const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        await console.log(response.data.sprites.front_default)
        this.frontSprite = await response.data.sprites.front_default
        console.log('typeof front', typeof(frontSprite))
        // return frontSprite
        // console.log(this.frontSprite)
      },
      anothaOne(frontURL) {
          console.log('typeof front in anotha', typeof(frontURL))
          this.frontSprite = frontURL
          console.log('anothaone', this.frontSprite)
      }
  }
}
</script>