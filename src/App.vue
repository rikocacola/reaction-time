<template>
  <h1>Reaction Timer</h1>
  <button @click="startPlay" :disabled="isPlaying">play</button>
  <Block
    v-if="isPlaying"
    :delay="delay"
    :isPlaying="isPlaying"
    @end="endGame"
    @wrong="wrongTime"
  />
  <Result v-if="showScore" :score="score" />
  <h3 v-if="tooSoon">Too Soon! Click play to try again!</h3>
</template>

<script>
import Block from "./components/Block";
import Result from "./components/Result";

export default {
  name: "App",
  data() {
    return {
      delay: null,
      isPlaying: false,
      score: null,
      showScore: false,
      tooSoon: false,
    };
  },
  components: { Block, Result },
  methods: {
    startPlay() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showScore = false;
      this.tooSoon = false;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showScore = true;
    },
    wrongTime() {
      this.isPlaying = false;
      this.delay = null;
      this.tooSoon = true;
    },
  },
};
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
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
