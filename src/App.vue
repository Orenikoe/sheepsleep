<template>
  <InstructionsComp @confirmInstructions="approveGame" v-if="!readInstructions && !gameEnded"/>
    <GameComp @gameEnd="handleEndGame" v-if="readInstructions"/>
  <SuccessComp v-show="gameEnded"/>
</template>

<script>
import GameComp from './components/GameComp.vue'
import InstructionsComp from './components/InstructionsComp.vue';
import SuccessComp from './components/SuccessComp.vue';
import {ref} from 'vue'

export default {
  name: 'App',
  setup() {
    let readInstructions = ref(false)
    let gameEnded = ref(false)
    const approveGame = (data) => {
      readInstructions.value = data

    }
    const handleEndGame = (data) => {
      if (data) {
        gameEnded.value = true
        readInstructions.value = false
      }

    }
    return {
      readInstructions,
      approveGame,
      gameEnded,
      handleEndGame
    }
  },
  components: {
    InstructionsComp,
    GameComp,
    SuccessComp
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
