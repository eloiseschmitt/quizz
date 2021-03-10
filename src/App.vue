<template>
  <HeaderApp :logo-link="state.logo.url" :logo-width="state.logo.width"/>
  <OptionsSelect @category-chosen="setCategoryChosen" @level-chosen="setLevelChosen"/>
  <Question :question-details="state.question"/>
</template>

<script>
import { reactive } from 'vue';
import HeaderApp from './components/Header'
import OptionsSelect from './components/OptionsSelect'
import Question from './components/Question'

const apiUrl = "https://www.openquizzdb.org/api.php"
const apiKey = "CW369ZE3QZ"

export default {
  name: 'App',
  components: {
    HeaderApp,
    OptionsSelect,
    Question
  },
  setup() {
    const state = reactive({
      logo: {
        url: "logo_large.png",
        width: 80
      },
      question: {},
      apiCall: {
        category: "",
        level: ""
      }
    });

    function setCategoryChosen(category) {
      if (category) state.apiCall.category = category
      callApi();
    }

    function setLevelChosen(level) {
      if (level) state.apiCall.level = level
      callApi();
    }

    function callApi() {
      if (state.apiCall.category && state.apiCall.level) {
        fetch(apiUrl + '?key=' + apiKey + '&categ=' +  state.apiCall.category + '&diff=' + state.apiCall.level)
        .then(blob => blob.json())
        .then(response => {
          if (response.response_code === 0) {
            state.question = response.results[0]
          }
        })
        .catch(error => console.log(error))
      }
    }
    
    return {
      state,
      setCategoryChosen,
      setLevelChosen,
      callApi
    }
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
