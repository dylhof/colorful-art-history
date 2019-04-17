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
    height: 155px;
    width: 155px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px;
    border: 2px solid black;  
  }

  .colors:hover {
    cursor: pointer;
  }
  
  p {
    text-shadow: 1px 1px 1px #dad6d6;
    font-size: 11px;
    letter-spacing: 2px;
  }
</style>
