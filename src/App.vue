<template>
  <MovieView />
</template>

<script>
import MovieView from "./components/MovieView.vue";
export default {
  name: "App",
  components: {
    MovieView,
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
