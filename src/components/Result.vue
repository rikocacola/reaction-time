<template>
  <h4>Reaction Time : {{ score }} ms</h4>
  <h2>{{ rank }}</h2>
</template>

<script>
export default {
  props: ["score"],
  data() {
    return {
      rank: "",
    };
  },
  mounted() {
    if (this.score < 250) {
      this.rank = "Great!";
    } else if (this.score < 400) {
      this.rank = "Nice!";
    } else {
      this.rank = "Bad!";
    }
  },
};
</script>