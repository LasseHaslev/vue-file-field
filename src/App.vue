<template>
  <div id="app">
    <img src="./assets/logo.png">
    <file-field :multiple="true" accept="image/*" name="image"></file-field>
    <file-field :multiple="true" name="image"></file-field>
  </div>
</template>

<script>
import FileField from './components/FileField.vue'

export default {
  name: 'app',
  components: {
    FileField
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
