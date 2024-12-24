
<template>
  <div class="layer-switcher">
    <div class="layer-list">
      <div
        v-for="(layer, index) in layers"
        :key="index"
        class="layer-item"
        :class="{ active: activeLayerIndex === index }"
        @click="switchLayer(index)"
      >
        <img :src="layer.image" alt="layer.name" class="layer-icon" />
        <span>{{ layer.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import { onMounted, ref } from "vue";
import { layerList } from "./layerList";
import { ElMessage } from "element-plus";
export default {
  name: "LayerSwitch",
  props: {
    viewer: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    // 图层数据，包括名称、图标图片和链接
    const layers = ref(layerList);

    // 当前激活的图层索引
    const activeLayerIndex = ref(0);

    // 切换图层
    const switchLayer = (index) => {
      activeLayerIndex.value = index;
      const selectedLayer = layers.value[index];
      addLayerToViewer(selectedLayer.url);
      copyUrl(selectedLayer.url);
    };
    const copyUrl = (url) => {
      //复制URL到剪贴板
      const input = document.createElement("input");
      input.value = url;
      document.body.appendChild(input);
      input.select();
      document.execCommand("copy");
      input.remove();

      ElMessage({
        message: url + " 已复制到剪贴板",
        type: "success",
      });
    };

    // 添加选中的图层到 Cesium viewer
    const addLayerToViewer = (url) => {
      const imageryLayerCollection = props.viewer.imageryLayers;

      // 移除当前所有图层
      imageryLayerCollection.removeAll();

      // 添加新的图层
      props.viewer.imageryLayers.addImageryProvider(
        new Cesium.UrlTemplateImageryProvider({
          url: url,
        })
      );
    };

    // 初始化时默认加载第一个图层
    onMounted(() => {
      addLayerToViewer(layers.value[activeLayerIndex.value].url);
    });

    return {
      layers,
      activeLayerIndex,
      switchLayer,
    };
  },
};
</script>

<style scoped>
.layer-switcher {
  position: absolute;
  bottom: 70px;
  right: 50px;
  z-index: 10;
  background-color: rgba(255, 255, 255, 0.7);
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.layer-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.layer-item {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.layer-item.active {
  background-color: rgba(0, 0, 0, 0.1);
}

.layer-icon {
  width: 20px;
  height: 20px;
  margin-right: 10px;
}

.layer-item span {
  font-size: 14px;
  font-weight: bold;
}
</style>
