<template>
    <main>
        <div>
            <h1>Who's that Pokémon?</h1>
            <img class='silhouette' :src="frontSprite"/>

          <form class="input-container" id="guess-form" onsubmit="return false;">
            <label class="all-access" for="guess-field">Type your guess here.</label>
            <input
            v-model='userGuess'
            id="guess-field" 
            class="guess-input" 
            name="guess-field" 
            type="search" 
            placeholder="Guess"/>
            <button
            @click='correctOrNah(userGuess)'
            id="guess-button"
            type="submit"><span class="all-access">Submit your guess</span>GO</button>
        </form>

        <div 
        v-if="incorrectGuess"
        class='failDiv'>
          <h2>Guess again!</h2>
        </div>
        
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
          randomInt: 0,
          incorrectGuess: false,
          min: 1,
          max: 151
      }
  },
  mounted() {
    this.getFrontSprite(this.getRandomInt())
  },
  methods: { 
      getRandomInt() {
          return Math.floor(Math.random() * (this.max - this.min + 1) + this.min);
      },
      getFrontSprite(id) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(response =>
            (this.frontName = response.data.name.replace(/\-.*/, ''),
            this.frontSprite = response.data.sprites.front_default));
      },
      clearInput() {
        this.userGuess = '';
      },
      correctOrNah(guess) {
        if (guess.toLowerCase() != this.frontName) {
          this.incorrectGuess = true
        }
        else {
          this.getFrontSprite(this.getRandomInt());
          this.incorrectGuess = false
        }
        this.clearInput();
      }
  }
}
</script>