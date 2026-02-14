<script setup lang="ts">
import { onMounted, ref } from 'vue';

const props = defineProps({
  images: Array<string>
});

const canvasElement = ref<HTMLCanvasElement | null>(null);
const canvasContext = ref<CanvasRenderingContext2D | null>(null);
const canvasSize = {
  width: 800,
  height: 600
};

let imageElements = [];


onMounted(() => {
  initializeCarousel();
});


const initializeCarousel = () => {
  canvasContext.value = canvasElement.value.getContext("2d");
  loadImages();
}

const loadImages = () => {
  imageElements = [];

  props.images.forEach((item) => {
    const currentElement = new Image();
    currentElement.src = item;
    currentElement.style.objectFit = "scale-down";
    currentElement.onload = () => {
      imageElements.push(currentElement);
      renderImages();
    }
  });
}

const renderImages = () => {
  imageElements.forEach((item) => {
    canvasContext.value.drawImage(item, 0, 0, canvasSize.width, canvasSize.height);
  });
}
</script>

<template>
  <canvas ref="canvasElement" width="800" height="600"></canvas>
</template>

<style scoped>
canvas {
  border: 1px solid green;
}
</style>