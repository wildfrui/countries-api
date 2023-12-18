<template>
  <FetchCountries/>
</template>

<script>
import FetchCountries from './components/FetchCountries.vue'

export default {
  name: 'App',
  components: {
    FetchCountries
  }
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
