<template>
  <div id="app">
    <signature />
  </div>
</template>

<script>
import Signature from './components/Signature.vue'
export default {
  components: { Signature },
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
