<template>
  <div id="app">
    <img src="./assets/logo.png">
    <image-field :multiple="true" accept="image/*" name="image"></image-field>
    <image-field :multiple="true" name="image"></image-field>
  </div>
</template>

<script>
import ImageField from './components/ImageField.vue'

export default {
  name: 'app',
  components: {
    ImageField
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
