<template>
  <div class="backgroundImage">
    <img class="background" src="./assets/Background.png">
  </div>
  <mothers-day></mothers-day>
</template>

<script>
import MothersDay from './components/MothersDay.vue'

export default {
  name: 'App',
  components: {
    MothersDay
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
.backgroundImage {
  position:fixed;
  left:0;
  right:0;
  top:0;
  bottom:0;
  z-index:-1;
}
.background {
  height: 100%;
  width: 100%;
}
</style>
