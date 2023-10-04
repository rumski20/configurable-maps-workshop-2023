<!-- src/components/AppHeader.vue -->
<script lang="ts" setup>
import { useAppStore } from "@/stores/app";
import DarkModeToggle from "@/components/DarkModeToggle.vue";

const appStore = useAppStore();
</script>

<template>
  <header>
    <nav :class="`navbar navbar-${appStore.theme} app-navbar bg-primary`">
      <div class="container-fluid">
        <span class="float-right d-flex justify-content-between mt-1">
          <font-awesome-icon
            v-if="!appStore.isSmallDevice"
            icon="fa-solid fa-list"
            color="white"
            @click="appStore.togglePanel('left')"
          />
        </span>
        <span class="navbar-brand mb-0 h1 text-light">Timeline Mapper</span>

        <span
          class="float-right d-flex justify-content-between mt-1 align-middle"
        >
          <dark-mode-toggle />
          <font-awesome-icon
            v-if="!appStore.isSmallDevice"
            icon="fa-solid fa-bars"
            color="white"
            class="mt-1"
            @click="appStore.togglePanel('right')"
          />
        </span>
      </div>
    </nav>
  </header>
</template>
