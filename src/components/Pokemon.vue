<template>
    <main>
        <div id='pokemon'>
            <h1 class='title' v-if='silhouette'>Who's that Pokémon?</h1>
            <div 
            v-if="!silhouette"
            class='failDiv'>
                <h1 class='title'>It's <span class='uppercase'>{{frontName}}!</span></h1>
            </div>
            <img 
            class='img'
            :class="{ silhouette: silhouette }"
            :src="frontSprite"/>

          <form
          class="input-container" 
          id="guess-form" 
          onsubmit="return false">
            <label class="all-access" for="guess-field">Type your guess here.</label>
            <input
            v-model='userGuess'
            id="guess-field" 
            class="guess-input" 
            name="guess-field" 
            type="search" 
            placeholder="Guess"/>
            <button
            class='uppercase'
            @click.prevent='correctOrNah(userGuess)'
            id="guess-button"
            type="submit"><span class="all-access">Submit your guess</span>Go</button>
          <div class='surrenderContainer'>
            <button
            @click.prevent='displaySpriteName()'
            type='submit'
            class='surrenderButton'>
            I give up!
            </button>
          </div>
        </form>

        <div 
        v-if="incorrectGuess"
        class='failDiv'>
          <h2 class='title'>Guess again!</h2>
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
          silhouette: true,
          min: 1,
          max: 151
      }
  },
  mounted() {
    this.getFrontSprite();
  },
  methods: { 
      getFrontSprite() {
        let randInt = Math.floor(Math.random() * (this.max - this.min + 1) + this.min);
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${randInt}/`)
        .then(response =>
            (this.frontName = response.data.name.replace(/\-.*/, ''),
            this.frontSprite = response.data.sprites.front_default));
        this.silhouette = true;
      },
      clearInput() {
        this.userGuess = '';
      },
      correctOrNah(guess) {
        if (guess.toLowerCase() != this.frontName) {
          this.incorrectGuess = true
        }
        else {
          this.displaySpriteName();
        }
        this.clearInput();
      },
      displaySpriteName() {
        this.incorrectGuess = false
        this.silhouette = false
        setTimeout(() => this.getFrontSprite(), 2000);
      }
  }
}
</script>