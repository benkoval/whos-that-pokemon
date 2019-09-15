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

@import url('https://fonts.googleapis.com/css?family=Press+Start+2P&display=swap');
@import url(https://fonts.googleapis.com/css?family=VT323);
$gameFont: 'Press Start 2P', cursive;
$btnFont: 'VT323', monospace;

#pokemon {
  text-align: center;
}

.title {
  font-family: $gameFont;
  color: #2c3e50;
  margin-top: 60px;
}
.surrenderButton {
  font-family: $btnFont;
	background: #881400;
	border-bottom: 5px inset rgba(0,0,0,.5);
	border-left: 5px inset rgba(0,0,0,.5);
	border-right: 5px inset rgba(255,255,255,.5);
	border-top: 5px inset rgba(255,255,255,.5);
	box-sizing: border-box;
	color: white;
	cursor: pointer;
	font-size: 1.8rem;
	margin: auto;
	min-width: 150px;
	padding: .3rem;
	text-transform: uppercase;
	
	&:focus,
	&:hover {
		background: #A81000;
	}

  &:active {
    translate: 8px;
  }
}

.surrenderContainer {
  display: flex;
}
.uppercase {
  text-transform: uppercase;
  margin-bottom: 40px;
}
// .img {
//   height: 40vh;
// }
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
