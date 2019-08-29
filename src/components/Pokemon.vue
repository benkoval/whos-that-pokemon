<template>
    <main>
        <div>
            <h1>ayyylmao</h1>
            <img class='silhouette' :src="frontSprite"/>
            <input
            id='inputGuess'
            placeholder='press enter asshole'
            type='text'
            v-model='userGuess'
            v-on:keyup.enter="getFrontSprite(getRandomInt())"/>
            <button
            :disabled='userGuess != frontName'
            @click='getFrontSprite(getRandomInt())'>Who's That Fuckin' Pokemon?!</button>

            <!-- <button
            @click='getBackSprite(getRandomInt())'>booty view</button>
            <img class='silhouette' :src="backSprite"/> -->
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
          frontName: '',
          userGuess: '',
        //   backSprite: '',
          randomInt: 0
      }
  },
//   mounted() {
//     this.getFrontSprite(this.getRandomInt())
//   },
  methods: { 
      getRandomInt() {
          return Math.floor(Math.random() * Math.floor(34))
        //   document.querySelector('#inputGuess').reset();
        //   console.log(guessInput.value)
        //   guessInput.value = '';
        //   return Math.random() * (28 - 1) + 28;
      },
      getFrontSprite(id) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(response =>
            (this.frontName = response.data.name,
            this.frontSprite = response.data.sprites.front_default));
            console.log(this.frontName)
      },
    //   getBackSprite(id) {
    //     axios
    //     .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
    //     .then(response =>
    //         (this.backSprite = response.data.sprites.back_default));
    //         console.log(this.backSprite)
    //   }
  }
}
</script>