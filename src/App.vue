<template>
  <div id="app">
    <h1>Coding Challenge</h1>
    <Hackathon/>
  </div>
</template>

<script>
import Hackathon from './components/Hackathon.vue'

export default {
  name: 'App',
  components: {
    Hackathon
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
  margin: 60px;
}
</style>
