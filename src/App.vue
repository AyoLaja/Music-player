<template>
  <div id="app">
    <MusicPlayer/>
  </div>
</template>

<script>
import MusicPlayer from './components/MusicPlayer.vue'
export default {
  name: 'App',
  components: {
    MusicPlayer
  }
}
</script>

<style lang="css" src="./styles/styles.css"></style>
<style>
#app {
  position: relative;
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  height: inherit;
}
</style>
