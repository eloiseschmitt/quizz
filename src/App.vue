<template>
  <HeaderApp :logo-link="state.logo.url" :logo-width="state.logo.width"/>
  <OptionsSelect @category-chosen="apiCall"/>
  <Question :question-details="state.question"/>
</template>

<script>
import { reactive } from 'vue';
import HeaderApp from './components/Header'
import OptionsSelect from './components/OptionsSelect'
import Question from './components/Question'

const apiUrl = "https://www.openquizzdb.org/api.php"
const apiKey = "CW369ZE3QZ"
//?key=4DH83PMR5B&categ=musique&diff=3

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
      question: ''
    });

    function apiCall(category) {
      fetch(apiUrl + '?key=' + apiKey + '&categ=' +  category + '&diff=1')
        .then(blob => blob.json())
        .then(response => state.question = response.results[0])
        .catch(error => console.log(error))
    }
    
    return {
      state,
      apiCall
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
