<template>
  <div id="app">
    <Menu :range="range" :play="play" @togglePlay="togglePlay"></Menu>
    <Game :range="range" :play="play"/>
  </div>
</template>

<script>
import Game from './components/Game.vue'
import Menu from './components/Menu.vue'

export default {
  name: 'App',
  components: {
    Game,
    Menu
  },
  data(){
    return {
         range:{x:50,y:50},
         play:false
    }
 },
 methods:{
   togglePlay(){
     this.play = !this.play
     console.log(this.play)
   }
 }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}
</style>
