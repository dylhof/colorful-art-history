<template>
  <div class= "selectedColorArea">
    <h2>SelectedColors</h2>
      <div class="selectedColorArea-div"> 
        <div 
          class="selectedColor"
          v-for="(color, i) in selectedColors"
          :key="i"
          :style="{backgroundColor: color}">
        </div>
      </div>
      <button
        @click="$emit('fetch-art')">Find Colorful Art History</button>
  </div>
</template>

<script>
export default {
  name: 'SelectedColors',
  props: {
    selectedColors: Array
  }
}
</script>

<style scoped>
  .selectedColorArea {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .selectedColorArea-div {
    display: flex;
  }

  .selectedColor {
    height: 50px;
    width: 50px;
    border: 2px solid black;
    border-radius: 50%;
    margin: 2px;
  }
  
</style>