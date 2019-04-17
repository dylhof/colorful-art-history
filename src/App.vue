<template>
  <div id="app">
    <header><h1>Colorful Art History</h1></header>
    <div class="selectedColors">
      <SelectedColors
        v-if="selectedColors.length > 0"
        :selectedColors="selectedColors"
        @fetch-art="fetchArt"
      ></SelectedColors>
    </div>
    <div v-if="view === 'colors'" class="colorArea">
      <p class="blurb">Select as many colors as you like, then find how colorful Art History can be! </p>
      <div class="colorArea-div">
        <Colors v-for="(color, index) in colors" :key="index" :color="color" @add-color="addColor"></Colors>
      </div>
    </div>
    <div v-else-if="view === 'art'" >
      <div class="artArea">
        <button @click="backToColors">Back To Colors</button>
        <div class="paintingArea">
          <Art v-for="(artObject, index) in art" :key="index" :artObject="artObject"></Art>
        </div>
      </div>
    <button @click="fetchArt">Fetch More Art</button>
    </div>
  </div>
</template>

<script>
import Colors from "./components/Colors.vue";
import SelectedColors from "./components/SelectedColors.vue";
import Art from "./components/Art.vue";
import axios from "axios";

export default {
  name: "app",
  components: {
    Colors,
    SelectedColors,
    Art
  },
  data() {
    return {
      colors: [],
      nextArt: 1,
      maxArt: "",
      selectedColors: [],
      allArt: false,
      art: [],
      view: "colors"
    };
  },
  mounted() {
    axios
      .get(
        `https://api.harvardartmuseums.org/color?apikey=${
          process.env.VUE_APP_API_KEY
        }&size=150&sort=random`
      )
      .then(response => {
        this.colors = response.data.records;
      });
  },
  methods: {
    addColor: function(color) {
      if (!this.selectedColors.includes(color)) {
        this.selectedColors.push(color);
      }
    },
    backToColors: function() {
      this.view = "colors"
    },
    fetchArt: function() {
      // const colorString = this.selectedColors.join("|");
      axios
        .get(
          `https://api.harvardartmuseums.org/object?apikey=${
            process.env.VUE_APP_API_KEY
          }&classification=Paintings&size=100&sort=random&page=${this.nextArt}`
        )
        .then(response => {
          response.data.records.forEach(record => {

            if (record.images !== undefined && record.images.length !== 0) {
              const images = [];
              const people = [];
              record.images.forEach(image => images.push(image.baseimageurl));
              if (record.people !== undefined) {
                record.people.forEach(person => people.push(person.name));
              }
              const newRecord = {
                title: record.title,
                images: images,
                dates: record.dated,
                artists: people
              };
              this.art.push(newRecord);
            }
          });
          this.maxArt = response.data.info.pages;
        });
      this.selectedColors = [];
      this.view = "art";
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Arvo');

* {
  font-family: 'Arvo', serif;
}

body {
  margin: 0;
}

header {
  height: 100px;
  position: fixed;
  background-color: white;
  width: 100%;
}

.blurb {
  margin: 20px;
  font-size: 30px;
  text-align: center;
}

.colorArea-div,
.paintingArea {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.colorArea {
  padding-top: 175px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.artArea {
  padding-top: 150px;
}

.selectedColors {
  position: fixed;
  background-color: white;
  width: 100%;
  top: 100px;
}

button {
  height: 30px;

}

h1{
  margin: 20px;
}
</style>
