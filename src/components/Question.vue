<template>
  <div>
    {{ questionDetails.question }}
    <form action="" @submit.prevent="validateAnswer">
      <select v-model="state.answer">
        <option
          :value="suggestion"
          v-for="(suggestion, i) in questionDetails.autres_choix"
          :key="i"
        >
          {{ suggestion }}
        </option>
      </select>
      <button type="submit">Valider</button>
    </form>
    <p v-if="state.displayAnswer" :class="{'--green': correct, '--red': !correct }">Réponse: {{ questionDetails.reponse_correcte }}</p>
  </div>
</template>

<script>
import { reactive } from "vue";

export default {
  name: "Question",
  props: {
    questionDetails: Object,
  },
  setup(props) {
    const state = reactive({
      answer: "",
      correct: true,
      displayAnswer: false,
    });

    function validateAnswer() {
        if (state.answer && state.answer !== props.questionDetails.reponse_correcte) {
            state.correct = false;
        }
        state.displayAnswer = true;
    }

    return {
      state,
      validateAnswer
    };
  },
};
</script>

<style lang="scss" scoped>
    .--green {
        color: green;
    }
    .--red {
        color: red;
    }
</style>