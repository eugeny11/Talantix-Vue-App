<template>
  <div id="app">
    <ShiftSelector />
  </div>
</template>

<script>
import ShiftSelector from './components/ShiftSelector.vue'

export default {
  name: 'App',
  components: {
    ShiftSelector
  }
}
</script>

<style>
body {
    font-family: 'Arial', sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
}

#app {
    max-width: 800px;
    margin: 50px auto;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
