# Cesium

## 初始化

```sh
npm create vite vue3-cesium --template vue

npm i cesium vite-plugin-cesium vite -D
```

在vite.config.js文件中添加cesium的插件

```js
import { defineConfig } from 'vite';
import cesium from 'vite-plugin-cesium';
export default defineConfig({
  plugins: [cesium()]
});
```

vue

```vue
<script setup>
  import { onMounted, ref } from 'vue'
  import * as Cesium from 'cesium'

  const initCesium = () => {
    Cesium.Ion.defaultAccessToken =
      'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI4ZjRiOWJjYS05YjFlLTQwMDItODJlMy1iNzNkODU5NDJiMjIiLCJpZCI6Mjg1NjUyLCJpYXQiOjE3NDIzNjYzODB9._KJdWwzj8NIjoVImtrNdClZ3zqa44wo3qb5cOXdOpBU'
    //初始化Cesium
    const viewer = new Cesium.Viewer('cesiumContainer', {
      // terrainProvider: Cesium.createWorldTerrain(),
      infoBox: false,
      selectionIndicator: false,
      timeline: false,
      animation: false,
      baseLayerPicker: false,
      geocoder: true,
      navigationHelpButton: false,
      sceneModePicker: false,
    })
  }
  //cesium初始化必须写在mounted生命周期里面，否则会报错"Element with id "cesiumContainer" does not exist in the document."
  onMounted(() => {
    initCesium()
  })
</script>

<template>
  <div id="cesiumContainer"></div>
</template>


<style scoped>
  #cesiumContainer {
    width: 100vw;
    height: 100vh;
  }
  *:deep(.cesium-viewer-bottom) * {
    display: none !important;
  }
</style>
```

