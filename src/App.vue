<template>
  <GameComp/>
</template>

<script>
import GameComp from './components/GameComp.vue'

export default {
  name: 'App',
  components: {
    GameComp
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
}

body{
  margin: 0px;
}
</style>
