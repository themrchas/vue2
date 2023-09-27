<template>
  <h1>reactiontimer</h1>
   
    <!-- :disabled is an attribute of button  - HTML specific-->
    <button type="button" @click="start" :disabled="isPlaying">Play</button>

    <!-- delay is a prop sent to Block; 
        @end is the event that was emitted from child; can be named anything you want
        endGame is the function that is run when event emitted from Block child
    -->
    <Block v-if="isPlaying" :delay="delay" @end="endGame"/>

    <h3 v-if="showResults">App (Parent)  - Reaction time is {{ reactionTime }} ms</h3>

</template>

<script>

import Block from './components/Block.vue'

export default {
  name: 'App',
  components: { Block  },
  data() {
    return {

      //Is user currently playing
      isPlaying: false,

      //Amount of time before block appears on the screen
      delay: 0,

      reactionTime: 0,

      showResults: false
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = !this.isPlaying;
    },

    //Note how reactionTime below is the data emitted by Block
    endGame(reactionTime) {
      this.reactionTime = reactionTime;
      this.isPlaying = !this.isPlaying
      this.showResults = !this.isPlaying
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
  color: #444;
  margin-top: 60px;
}
</style>
