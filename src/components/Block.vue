<template>
  <div class="block" v-if="showBlock" @click="stopTimer">click me</div>
  <div
    class="block"
    v-if="isPlaying && showBlock === false"
    :style="{ backgroundColor: 'red' }"
    @click="wrongClick"
  >
    Wait for green!
  </div>
</template>

<script>
export default {
  props: ["delay", "isPlaying"],
  emits: ["end", "wrong"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit("end", this.reactionTime);
    },
    wrongClick() {
      clearInterval(this.timer);
      this.$emit("wrong");
    },
  },
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
  cursor: pointer;
}
</style>