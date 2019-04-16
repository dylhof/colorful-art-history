<template>
  <div 
    class="colors" 
    :style="{backgroundColor: color.hex}"
    @click="$emit('add-color', color.hex)">
    <p>{{color.name}}</p>
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
