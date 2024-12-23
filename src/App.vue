<template>
  <OnlineMap msg="Welcome to Your Vue.js App" />
</template>

<script>
import OnlineMap from "./components/OnlineMap.vue";

export default {
  name: "App",
  components: {
    OnlineMap,
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
</style>
