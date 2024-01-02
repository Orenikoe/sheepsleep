<template>
  <InstructionsComp @confirmInstructions="approveGame" v-if="!readInstructions"/>
  <GameComp v-if="readInstructions"/>
</template>

<script>
import GameComp from './components/GameComp.vue'
import InstructionsComp from './components/InstructionsComp.vue';
import {ref} from 'vue'

export default {
  name: 'App',
  setup() {
    let readInstructions = ref(false)
    const approveGame = (data) => {
      readInstructions.value = data

    }
    return {
      readInstructions,
      approveGame
    }
  },
  components: {
    InstructionsComp,
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
