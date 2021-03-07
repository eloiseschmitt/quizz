<template>
  <HeaderApp :logo-link="state.logo.url" :logo-width="state.logo.width"/>
</template>

<script>
import { reactive } from 'vue';
import HeaderApp from './components/Header'

export default {
  name: 'App',
  components: {
    HeaderApp
  },
  setup() {
    const state = reactive({
      logo: {
        url: "logo_large.png",
        width: 80
      }
      
    })
    
    return {
      state
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
