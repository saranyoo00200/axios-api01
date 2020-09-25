<template>
  <div id="app">
    <musics />
  </div>
</template>

<script>
import musics from "./components/musics.vue";

export default {
  name: "App",
  components: {
    musics,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background-image: url("../src/assets/33270.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  margin-top: 50px;
}
</style>
