<template>
  <div id="app"> 
    <div class="colorArea">
      <Colors v-for="(color, index) in colors" :key="index" :color="color"></Colors>
    </div>
    <button @click="fetchColors">Fetch More Colors</button>
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
        this.nextColors = 2
      })
  },
  methods: {
    fetchColors: function() {
      axios
        .get(`https://api.harvardartmuseums.org/color?apikey=${process.env.VUE_APP_API_KEY}&page=${this.nextColors}`)
        .then(response => {
          response.data.records.forEach(color => this.colors.push(color));
          this.nextColors++
        })

    }
  }
}
</script>

<style>
  .colorArea {
    display: flex;
    flex-wrap: wrap;
  }
</style>
