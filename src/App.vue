<template>
  <div id="gif">
    <GiphyViewer/>
  </div>
</template>

<script>
import GiphyViewer from './components/GiphyViewer.vue'

export default {
  name: 'App',
  components: {
    GiphyViewer
  }
}
</script>

<style>
   #gif {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
