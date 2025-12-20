<script setup>
import mapImage from '../assets/map.png'

const props = defineProps({
  properties: {
    type: Array,
    required: true,
  },
})
</script>

<template>
  <div class="map-container">
    <img :src="mapImage" alt="US Map" class="map-image" />
  </div>
</template>

<style>
.map-container {
  width: 100%;
  height: 100%;
  border-radius: 0;
  overflow: hidden;
  background-color: var(--color-gray-100);
}

.map-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
</style>
