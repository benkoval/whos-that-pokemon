<template>
    <main>
        <div>
            <h1>Who's that Pokémon?</h1>
            <img class='silhouette' :src="frontSprite"/>

          <form class="input-container" id="guess-form">
            <label class="all-access" for="guess-field">Type your guess here.</label>
            <input
            @keyup.enter='clearInputOnSubmit()'
            v-model='userGuess'
            id="guess-field" 
            class="guess-input" 
            name="guess-field" 
            type="search" 
            placeholder="Guess"/>
            <button
            @click.prevent='correctOrNah(userGuess), clearInputOnClick()'
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
            // console.log(this.frontName)
      },
      clearInputOnSubmit() {
        document.querySelector('#guess-form').reset();
        document.querySelector('#guess-field').value = '';
      },
      clearInputOnClick() {
        document.querySelector('#guess-form').reset();
        document.querySelector('#guess-field').value = '';
      },
      correctOrNah(guess) {
        // this.clearInput()
        // const input = document.querySelector('#guess-field');
        // console.log('before', input.value);
        // input.textContent = '';
        // console.log('after', input.value);
        if (guess.toLowerCase() != this.frontName) {
          this.incorrectGuess = true
          console.log('after in if', document.querySelector('#guess-field').value);
        }
        else {
          this.getFrontSprite(this.getRandomInt());
          this.incorrectGuess = false
          console.log('after in if', document.querySelector('#guess-field').value);
        }
      }
  }
}
</script>