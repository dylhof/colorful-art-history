<template>
<div class="art">
  <div 
    v-if="artObject.images.length">
    <img 
      
      :key="index"
      :src="artObject.images[0]"
      :alt="artObject.title"
    />
    <div>
      <p class="title">{{artObject.title}}</p>
      <p v-for="(artist, index) in artObject.artists">{{artist}}</p>
    </div>
  </div>
</div>
</template>

<script>
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
  }

  .art {
    display: flex;
  }
</style>