<template>
  <body class="bg">
    <div>
      <b-container>
        <b-row>
          <b-col>
            <GiphyViewer />
          </b-col>
        </b-row>
      </b-container>
    </div>
  </body>
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
  .container {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #fefefe;
  }

  .bg {
    background-color: black;
  }
</style>