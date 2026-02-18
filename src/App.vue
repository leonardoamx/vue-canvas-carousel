<script setup lang="ts">
import { ref } from 'vue';
import CanvasImageCarousel from './components/CanvasImageCarousel.vue';

const imagesList = ref([
  "https://picsum.photos/2000/1000",
  "https://picsum.photos/2000/1500",
  "https://picsum.photos/2000/4000",
  "https://picsum.photos/2000/3000",
  "https://picsum.photos/2000/2000",
  "https://picsum.photos/1200/5000",
]);
</script>

<template>
  <h1>Canvas image carousel demo</h1>
  <p>
    Objective: Render a set of images on a canvas element and create a carousel effect by transitioning between them. The carousel should automatically cycle through the images every few seconds, and users should also have the option to manually navigate through the images using buttons or swipe gestures.
  </p>

  <CanvasImageCarousel :images="imagesList" />
</template>

<style scoped></style>
