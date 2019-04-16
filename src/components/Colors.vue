<template>
  <div>
    <div class="colors" v-bind:style="{backgroundColor: color.hex}">
      <p>{{color.name}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Colors',
  props: {
    color: Object
  }
}
</script>

<style scoped>
  .colors {
    height: 150px;
    width: 150px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px;
    border: 2px solid black;  
  }
</style>
