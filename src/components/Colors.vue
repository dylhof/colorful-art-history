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
    border: 2px solid #4e4c4c52;  
  }

  .colors:hover {
    cursor: pointer;
  }

  p {
    text-shadow: 1px 1px 1px whitesmoke;
    font-size: 11px;
    letter-spacing: 2px;
  }
</style>
