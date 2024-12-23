<template>
  <div id="cesiumContainer"></div>
</template>

<script>
/* eslint-disable */
import "../../public/Cesium/Widgets/widgets.css";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      viewer: null,
    };
  },
  methods: {
    initCesium() {
      // Create a new Viewer object
      this.viewer = new Cesium.Viewer("cesiumContainer");
    },
  },
  mounted() {
    this.initCesium();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
