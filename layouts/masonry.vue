<template>
  <div class="slidev-layout default">
    <div class="mb-4 relative z-10">
      <slot />
    </div>

    <div class="masonry-gallery">
      <img
        v-for="(img, idx) in images"
        :key="img"
        :src="img"
        :class="{ expanded: $clicks === idx + 1 }"
        :alt="'Gallery Image ' + (idx + 1)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
// Определяем входные параметры (props)
defineProps({
  images: {
    type: Array,
    default: () => [],
  },
});
</script>

<style>
/* Основные стили страницы */
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  display: flex;
  justify-content: center;
  padding: 20px;
}

/* --- СТИЛИ ГАЛЕРЕИ --- */
.masonry-gallery {
  width: 100%;
  max-width: 1000px;
  column-count: 3;
  column-gap: 15px;
}

.masonry-gallery img {
  width: 100%;
  border-radius: 12px;
  margin-bottom: 15px;
  display: block;
  break-inside: avoid;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);

  transition: transform 0.3s ease;
  cursor: pointer;

  position: relative;
  z-index: 1;
}

.masonry-gallery img.expanded {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  width: 90vw;
  height: 90vh;

  object-fit: contain;

  z-index: 9999;
  border-radius: 8px;
  background-color: transparent;

  animation: zoomIn 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes zoomIn {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.1);
  }
  100% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(0.6);
  }
}

@media (max-width: 768px) {
  .masonry-gallery {
    column-count: 2;
  }
}
@media (max-width: 480px) {
  .masonry-gallery {
    column-count: 1;
  }
}
</style>
