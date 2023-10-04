<!-- src/views/MapView.vue -->
<script lang="ts" setup>
import { ref, onMounted } from "vue";
import { useMap } from "@/composables";

const esriMap = ref();

onMounted(() => {
  const { view, map } = useMap(esriMap.value);
});
</script>

<template>
  <div class="map-wrapper">
    <div id="esri-map" ref="esriMap"></div>
  </div>
</template>

<style lang="scss">
.map-wrapper {
  width: 100%;
  height: calc(100vh - 300px);
}

#esri-map {
  height: 100%;
  width: 100%;
}
</style>
