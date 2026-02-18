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
const initialPointerPosition = {
  x: 0,
  y: 0
};
const slidesPosition = {
  x: 0,
  y: 0
};

let imageElements: HTMLImageElement[] = [];
let isDragActive = false;


onMounted(() => {
  initializeCarousel();
});


const dragStart = (event: PointerEvent) => {
  isDragActive = true;
  initialPointerPosition.x = event.clientX;
  initialPointerPosition.y = event.clientY;
  console.log("drag start");
}

const dragStop = (event: PointerEvent) => {
  isDragActive = false;
  let deltaX = event.clientX - initialPointerPosition.x;
  slidesPosition.x += deltaX;
  console.log("drag stop");
}

const dragMove = (event: PointerEvent) => {
  if(!isDragActive) {
    return;
  }
  let deltaX = event.clientX - initialPointerPosition.x;
  renderImages(deltaX);
  console.log("drag move");
}

const initializeCarousel = () => {
  canvasContext.value = canvasElement.value?.getContext("2d") || null;
  loadImages();
}

const loadImages = () => {
  imageElements = [];

  props.images?.forEach((item) => {
    const currentElement = new Image();
    currentElement.src = item;
    currentElement.onload = () => {
      imageElements.push(currentElement);
      renderImages(0);
    }
  });
}

const renderImages = (deltaX: number) => {
  // Adjust carousel boundaries
  if(slidesPosition.x + deltaX > 0) {
    slidesPosition.x = 0;
    deltaX = 0;
  }
  if(slidesPosition.x + deltaX < -(canvasSize.width * (imageElements.length - 1)) ) {
    slidesPosition.x = -(canvasSize.width * (imageElements.length - 1));
    deltaX = 0;
  }

  canvasContext.value?.clearRect(0, 0, canvasSize.width, canvasSize.height);
  imageElements.forEach((item, index: number) => {
    let scale = Math.min(canvasSize.width / item.width, canvasSize.height / item.height);
    let itemSize = {
      width: item.width * scale,
      height: item.height * scale
    };
    let offset = {
      x: (canvasSize.width - itemSize.width) / 2 + deltaX + slidesPosition.x,
      y: (canvasSize.height - itemSize.height) / 2
    };
    let positionX = canvasSize.width * index
    canvasContext.value?.drawImage(item, positionX + offset.x, offset.y, itemSize.width, itemSize.height);
  });
}
</script>

<template>
  <canvas
    ref="canvasElement"
    @pointerdown="dragStart"
    @pointermove="dragMove"
    @pointerup="dragStop"
    @pointerleave="dragStop"
    width="800" height="600"
  ></canvas>
</template>

<style scoped>
canvas {
  border: 1px solid green;
}
</style>