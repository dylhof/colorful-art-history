<template>
  <div class="art">
    <img 
      key="uuid"
      :src="artObject.images[0]"
      :alt="artObject.title"/>
    <div >
      <p class="title">{{artObject.title}}</p>
      <p> {{artObject.dates}} </p>
      <div class="artists">
        <p v-for="(artist, index) in artObject.artists" :key="index">{{artist}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  import { uuid } from 'vue-uuid';
  export default {
    name: 'Art',
    props: {
      artObject: Object
    }
  }
</script>

<style scoped>
  img {
    height: 300px;
    width: 200px;
    object-fit: cover;
    box-shadow: 3px 3px 3px #4e4c4c52;
  }

  .art {
    display: flex;
    flex-direction: column;
    height: 420px;
    width: 200px;
    margin: 20px;
  }

  .title {
    max-height: 50px;
    overflow: scroll;
  }

  .artists {
    height: 30px;
    overflow: scroll;
  }

  p { 
    font-size: 11px;
  
  }
</style>