<template>
  <div id="app"> 
    <SelectedColors 
      v-if="selectedColors.length > 0"
      :selectedColors="selectedColors"
      @fetch-art="fetchArt">
    </SelectedColors>
    <div 
      v-if="view === 'colors'"
      class="colorArea">
      <Colors 
        v-for="(color, index) in colors" 
        :key="index" 
        :color="color"
        @add-color="addColor">
      </Colors>
    </div>
    <!-- <button @click="fetchColors">Fetch More Colors</button> -->
    <div
      v-else-if="view === 'art'"
      class="artArea">
      <button>Back To Colors</button>
      <Art
        v-for="(artObject, index) in art"
        :key="index"
        :artObject="artObject"></Art>
      
    </div>
  </div>
</template>

<script>
import Colors from './components/Colors.vue';
import SelectedColors from './components/SelectedColors.vue';
import Art from './components/Art.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Colors,
    SelectedColors,
    Art
  },
  data() {
    return{
      colors: [],
      nextColors: '',
      selectedColors: [],
      allColors: false,
      art: [],
      view: 'colors'
    }
  },
  mounted() {
    axios
      .get(`https://api.harvardartmuseums.org/color?apikey=${process.env.VUE_APP_API_KEY}&size=150&sort=random`)
      .then(response => {
        this.colors = response.data.records
        this.nextColors = 2
      })
  },
  methods: {
    // fetchColors: function () {
    //   if(this.nextColors <= 15) {
    //     axios
    //       .get(`https://api.harvardartmuseums.org/color?apikey=${process.env.VUE_APP_API_KEY}&page=${this.nextColors}`)
    //       .then(response => {
    //         response.data.records.forEach(color => this.colors.push(color));
    //         this.nextColors++
    //       })
    //   } else {
    //     this.allColors = true
    //   }
    // },
    addColor: function(color) {
      if(!this.selectedColors.includes(color)){
        this.selectedColors.push(color)
      }
    },
    fetchArt: function() {
      const colorString = this.selectedColors.join('|')
      axios
        .get(`https://api.harvardartmuseums.org/object?apikey=${process.env.VUE_APP_API_KEY}&classification=Paintings&size=100&sort=random`)
        .then(response => {
          response.data.records.forEach(record => {
            const images = []
            const people = []
            if(record.images !== undefined){
              record.images.forEach(image => images.push(image.baseimageurl))
            }
            if(record.people !== undefined) {
              record.people.forEach(person => people.push(person.name))
            }
            const newRecord = { title: record.title, images: images, dates: record.dated, artists: people}
            this.art.push(newRecord)
          })
        })
      this.selectedColors = []
      this.view = 'art'
    }
  }
}
</script>

<style>
  .colorArea,
  .artArea{
    display: flex;
    flex-wrap: wrap;
  }

  
</style>
