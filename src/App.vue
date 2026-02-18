<script setup lang="ts">
import { ref } from 'vue';
import CanvasImageCarousel from './components/CanvasImageCarousel.vue';

const imagesList = ref([
  "https://picsum.photos/2000/1500",
  "https://picsum.photos/2000/1000",
  "https://picsum.photos/2000/4000",
  "https://picsum.photos/2000/3000",
  "https://picsum.photos/2000/2000",
  "https://picsum.photos/1200/5000",
]);
</script>

<template>
  <div class="container">
    <h1>Canvas image carousel demo</h1>
    <p>
      Objective: Render a set of images on a canvas element and create a carousel.
      <br>
      Users should have the option to manually navigate through the images using swipe gestures.
    </p>

    <CanvasImageCarousel :images="imagesList" :width="800" :height="500" />

    <h2>Takeaways</h2>
    <p>
      Using the canvas API brought me back to my days using Flash Platform and distributing elements in the stage.
      A major feature I would like to implement next is improving the drag & drop process, adding snap to picture and inertia features, with Greensock animation engine.
    </p>
  </div>
</template>

<style scoped>
  .container {
    width: 100%;
    max-width: 1000px;
    margin: 0 auto;
    font: 12pt Aptos, Lato, Helvetica, Arial;
    color: hsl(200, 100%, 20%);
  }
</style>
