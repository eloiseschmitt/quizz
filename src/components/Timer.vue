<template>
  <h2>Temps restant avant de passer à la question suivante:</h2>
  <p>{{ state.seconds }} seconds</p>
</template>

<script>
import { reactive, onMounted } from "vue";

export default {
  name: "Timer",
  setup() {
    const state = reactive({
      seconds: 60,
    });

    onMounted(() => {
        decreaseTimer()
    });

    function decreaseTimer() {
      setInterval(() => {
        state.seconds--;
      }, 1000);
    }

    return {
      state,
      decreaseTimer
    };
  },
};
</script>

<style>
</style>