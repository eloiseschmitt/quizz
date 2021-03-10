<template>
  <div>
    {{ questionDetails.question }}
    <form
      action=""
      @submit.prevent="validateAnswer"
      v-if="questionDetails.question"
    >
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
    <div v-if="state.displayAnswer">
      <p v-if="state.correct">Bien joué !</p>
      <p v-else>Dommage !</p>
      <p :class="{ '--green': state.correct, '--red': !state.correct }">
        Réponse: {{ questionDetails.reponse_correcte }}
      </p>
    </div>
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
      if (
        state.answer &&
        state.answer !== props.questionDetails.reponse_correcte
      ) {
        state.correct = false;
      }
      state.displayAnswer = true;
    }

    return {
      state,
      validateAnswer,
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