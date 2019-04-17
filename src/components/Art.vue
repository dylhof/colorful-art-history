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
  }

  .art {
    display: flex;
    flex-direction: column;
    height: 420px;
    width: 300px;
    margin: 20px;
  }

  .title {
    height: 75px;
    overflow: scroll;
  }

  .artists {
    height: 30px;
    overflow: scroll;
  }
</style>