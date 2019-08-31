<template>
    <main>
        <div>
            <h1>Who's that Pokémon?</h1>
            <img class='silhouette' :src="frontSprite"/>

          <form class="input-container" id="guess-form">
            <label class="all-access" for="guess-field">Type your guess here.</label>
            <input
            v-model='userGuess'
            id="guess-field" 
            class="search-input" 
            name="guess-field" 
            type="search" 
            placeholder="Guess"/>
            <button
            :disabled='userGuess != frontName'
            @click.prevent='getFrontSprite(getRandomInt())'
            id="search-button"
            type="submit"><span class="all-access">Submit your </span>Guess</button>
        </form>
        
        <!-- <input
            id='inputGuess'
            placeholder='press enter asshole'
            type='text'
            v-model='userGuess'
            v-on:keyup.enter="getFrontSprite(getRandomInt())"/>
            <button
            :disabled='userGuess != frontName'
            @click='getFrontSprite(getRandomInt())'>Who's That Fuckin' Pokemon?!</button> -->

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
  mounted() {
    this.getFrontSprite(this.getRandomInt())
  },
  methods: { 
      getRandomInt() {
          return Math.floor(Math.random() * Math.floor(151))
      },
      getFrontSprite(id) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(response =>
            (this.frontName = response.data.name,
            this.frontSprite = response.data.sprites.front_default));
            console.log(this.frontName)
      }
  }
}
</script>