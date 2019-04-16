<template>
  <div id="app">
    
    <Colors msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Colors from './components/Colors.vue'

export default {
  name: 'app',
  components: {
    Colors
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
