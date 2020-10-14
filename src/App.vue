<template>
  <div id="app">
    <Landscape />
  </div>
</template>

<script>
import Landscape from "./components/landscape.vue";

export default {
  name: "App",
  components: {
    Landscape,
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
  margin-top: 60px;
}
</style>
