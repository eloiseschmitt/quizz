<template>
  <div>
    {{ questionDetails.question }}
    <select v-bind="suggestions">
      <option
        value="suggestion"
        v-for="(suggestion, i) in questionDetails.autres_choix"
        :key="i"
      >
        {{ suggestion }}
      </option>
    </select>
  </div>
</template>

<script>
import { reactive } from "vue";

export default {
  name: "Question",
  props: {
    questionDetails: Object,
  },
  setup() {
    const state = reactive({
      suggestion: "",
    });

    return {
      state,
    };
  },
};
</script>

<style>
</style>