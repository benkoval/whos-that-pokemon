<template>
    <main>
        <div>
            <h1 v-if='silhouette'>Who's that Pokémon?</h1>
            <div 
            v-if="!silhouette"
            class='failDiv'>
              <h1>It's <span class='uppercase'>{{frontName}}!</span></h1>
            </div>
            <img 
            class='img'
            :class="{ silhouette: silhouette, jackInTheBox: jackInTheBox }"
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
            @click.prevent='giveUp()'
            type='submit'
            class='surrenderButton'>
            I give up!
            </button>
          </div>
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
          silhouette: true,
          jackInTheBox: false,
          min: 1,
          max: 300
      }
  },
  mounted() {
    this.getFrontSprite(this.getRandomInt())
  },
  methods: { 
      getRandomInt() {
          let randInt = Math.floor(Math.random() * (this.max - this.min + 1) + this.min);
          return randInt;
      },
      getFrontSprite(id) {
        this.silhouette = true;
        this.jackInTheBox = true;
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(response =>
            (this.frontName = response.data.name.replace(/\-.*/, ''),
            this.frontSprite = response.data.sprites.front_default));
      },
      clearInput() {
        this.userGuess = '';
        this.jackInTheBox = false;
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
      },
      giveUp() {
        this.silhouette = false
        setTimeout(() => this.silhouette = true, 2000);
      }
  }
}
</script>