<!-- src/App.vue -->
<script setup lang="ts">
import "@/assets/font-awesome";
import "@/assets/styles/style.scss";

import { defineAsyncComponent } from "vue";
import { useAppStore } from "./stores";
import { useColorTheme } from "@/composables";

import Spinner from "./components/Spinner.vue";
import AppHeader from "@/components/AppHeader.vue";

const MapView = defineAsyncComponent(() => import("@/views/MapView.vue"));
const appStore = useAppStore();

const { setThemeColors } = useColorTheme();
setThemeColors(appStore.config.app.theme!);
</script>

<template>
  <div class="app container-fluid">
    <!-- header -->
    <div class="row app-navbar">
      <div class="col px-0">
        <AppHeader />
      </div>
    </div>

    <div class="row main-content-row">
      <!-- left panel -->
      <div
        v-if="appStore.leftPaneOpen && !appStore.isSmallDevice"
        class="col-md-3 col-xl-2 border sidebar"
      >
        sidebar
      </div>

      <!-- main section -->
      <div class="col">
        <Suspense>
          <MapView />
          <template #fallback>
            <div class="w-100 h-100" style="min-height: 700px">
              <Spinner class="mx-auto my-auto" />
            </div>
          </template>
        </Suspense>
      </div>

      <!-- right panel -->
      <div
        v-if="appStore.rightPaneOpen && !appStore.isSmallDevice"
        class="col-md-3 col-xl-2 border sidebar"
      >
        sidebar
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "@/assets/styles/variables";

.main-content-row {
  height: $max-height;
}

.app-navbar {
  height: $navbar-height;
}
</style>
