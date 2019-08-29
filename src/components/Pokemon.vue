<template>
    <main>
        <div>
            <h1>ayyylmao</h1>
            <button
            @click='getFrontSprite(getRandomInt())'>frontal view</button>
            <img class='silhouette' :src="frontSprite"/>

            <button
            @click='getBackSprite(getRandomInt())'>booty view</button>
            <img class='silhouette' :src="backSprite"/>
        </div>
    </main>
</template>

<script>
import axios from "axios";

export default {
  name: 'Pokemon',
  data () {
      return {
          frontSprite: '',
          backSprite: '',
          randomInt: 0
      }
  },
//   mounted() {
//     this.getFrontSprite(this.getRandomInt())
//   },
  methods: { 
      getRandomInt() {
          return Math.floor(Math.random() * Math.floor(251))
      },
      getFrontSprite(id) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(response =>
            (this.frontSprite = response.data.sprites.front_default));
            console.log(this.frontSprite)
      },
      getBackSprite(id) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(response =>
            (this.backSprite = response.data.sprites.back_default));
            console.log(this.backSprite)
      }
  }
}
</script>