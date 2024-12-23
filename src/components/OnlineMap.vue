<template>
  <div id="cesiumContainer">
    <!-- 使用 v-if 来确保 viewer 初始化完成后再渲染 LayerSwitch 组件 -->
    <LayerSwitch v-if="viewer" :viewer="viewer" />
  </div>
</template>

<script>
/* eslint-disable */
import { onMounted, ref } from "vue";
import "../../public/Cesium/Widgets/widgets.css";
import LayerSwitch from "./tools/layerSwitch.vue";

export default {
  name: "OnlineMap",
  components: {
    LayerSwitch,
  },
  setup() {
    // 创建响应式的 viewer 对象
    const viewer = ref(null);

    // 初始化 Cesium Viewer
    const initCesium = () => {
      viewer.value = new Cesium.Viewer("cesiumContainer");
    };

    // 使用 onMounted 生命周期钩子
    onMounted(() => {
      console.log("OnlineMap mounted");
      initCesium();
    });

    // 返回响应式数据和方法
    return {
      viewer,
    };
  },
};
</script>

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
