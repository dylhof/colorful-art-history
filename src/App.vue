<template>
  <div id="app">
    
    <Colors v-for="(color, index) in colors" :key="index" :color="color"></Colors>
  </div>
</template>

<script>
import Colors from './components/Colors.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Colors
  },
  data() {
    return{
      colors: [],
      nextColors: '',
      selectedColors: []
    }
  },
  mounted() {
    axios
      .get(`https://api.harvardartmuseums.org/color?apikey=${process.env.VUE_APP_API_KEY}`)
      .then(response => {
        this.colors = response.data.records
        this.nextColors = response.data.info.next
      })
  }
}
</script>

<style>

</style>
