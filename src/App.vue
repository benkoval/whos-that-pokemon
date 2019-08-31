<template>
  <div id="app">
    <Pokemon/>
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'app',
  components: {
    Pokemon
  }
}
</script>

<style lang='scss'>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.silhouette {
    filter: contrast(0) brightness(0);
    pointer-events: none;
}

.failText {
  font-size: 6rem;
  color: #000;
}
// Text meant only for screen readers.
.all-access {
	clip-path: rect(1px, 1px, 1px, 1px);
    height: 1px;
    width: 1px;
	overflow: hidden;
    position: absolute !important;
}
</style>
