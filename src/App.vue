<template>
  <div id="app"> 
    <SelectedColors 
      v-if="selectedColors.length > 0"
      :selectedColors="selectedColors"
      @fetch-art="fetchArt">
    </SelectedColors>
    <div class="colorArea">
      <Colors 
        v-for="(color, index) in colors" 
        :key="index" 
        :color="color"
        @add-color="addColor">
      </Colors>
    </div>
    <button @click="fetchColors">Fetch More Colors</button>
  </div>
</template>

<script>
import Colors from './components/Colors.vue';
import SelectedColors from './components/SelectedColors.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Colors,
    SelectedColors
  },
  data() {
    return{
      colors: [],
      nextColors: '',
      selectedColors: [],
      allColors: false,
      art: []
    }
  },
  mounted() {
    axios
      .get(`https://api.harvardartmuseums.org/color?apikey=${process.env.VUE_APP_API_KEY}&size=150`)
      .then(response => {
        this.colors = response.data.records
        this.nextColors = 2
      })
  },
  methods: {
    fetchColors: function () {
      if(this.nextColors <= 15) {
        axios
          .get(`https://api.harvardartmuseums.org/color?apikey=${process.env.VUE_APP_API_KEY}&page=${this.nextColors}`)
          .then(response => {
            response.data.records.forEach(color => this.colors.push(color));
            this.nextColors++
          })
      } else {
        this.allColors = true
      }
    },
    addColor: function(color) {
      if(!this.selectedColors.includes(color)){
        this.selectedColors.push(color)
      }
    },
    fetchArt: function() {
      const colorString = this.selectedColors.join('|')
      console.log(colorString)
      axios
        .get(`https://api.harvardartmuseums.org/object?apikey=${process.env.VUE_APP_API_KEY}&color=${colorString}`)
        .then(response => {
          console.log(response)
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
