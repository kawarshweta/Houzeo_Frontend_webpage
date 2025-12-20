<script setup>
import { ref, computed, onBeforeUnmount } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import LogoImage from '../assets/logo.png'

const props = defineProps({
  images: {
    type: Array,
    required: true,
  },
  isHovered: {
    type: Boolean,
    default: false,
  },
})

const currentIndex = ref(0)
const imageContainer = ref(null)
const isVisible = ref(false)
const loadedImages = ref(new Set())

// Lazy loading with Intersection Observer
const { stop } = useIntersectionObserver(
  imageContainer,
  ([{ isIntersecting }]) => {
    if (isIntersecting) {
      isVisible.value = true
      if (props.images.length > 0) {
        loadedImages.value.add(0)
      }
    }
  },
  { threshold: 0.1 }
)

// Cleanup on unmount
onBeforeUnmount(() => {
  stop()
})

const nextImage = () => {
  if (props.images.length === 0) return
  currentIndex.value = (currentIndex.value + 1) % props.images.length
  loadedImages.value.add(currentIndex.value)
  const nextIdx = (currentIndex.value + 1) % props.images.length
  loadedImages.value.add(nextIdx)
}

const prevImage = () => {
  if (props.images.length === 0) return
  currentIndex.value = currentIndex.value === 0 ? props.images.length - 1 : currentIndex.value - 1
  loadedImages.value.add(currentIndex.value)
  const prevIdx = currentIndex.value === 0 ? props.images.length - 1 : currentIndex.value - 1
  loadedImages.value.add(prevIdx)
}

const goToImage = (index) => {
  if (index < 0 || index >= props.images.length) return
  currentIndex.value = index
  loadedImages.value.add(index)
}

const shouldLoadImage = (index) => {
  return isVisible.value && (loadedImages.value.has(index) || index === 0)
}

const slideStyle = computed(() => ({
  transform: `translateX(-${currentIndex.value * 100}%)`,
}))
</script>

<template>
  <div ref="imageContainer" class="image-slider">
    <!-- Images Container -->
    <div
      class="slider-container"
      :style="slideStyle"
    >
      <div
        v-for="(image, index) in images"
        :key="index"
        class="slider-slide"
      >
        <img
          v-if="shouldLoadImage(index)"
          :src="image"
          :alt="`Property image ${index + 1}`"
          class="slider-image"
          loading="lazy"
        />
        <div
          v-else
          class="slider-placeholder"
        >
          <svg
            width="48"
            height="48"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            style="color: var(--color-gray-300);"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
            />
          </svg>
        </div>
      </div>
    </div>

    <!-- Navigation Arrows (shown on hover) -->
    <button
      v-if="images.length > 1 && isHovered"
      @click.stop="prevImage"
      class="slider-arrow slider-arrow-left"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M15 19l-7-7 7-7"
        />
      </svg>
    </button>

    <button
      v-if="images.length > 1 && isHovered"
      @click.stop="nextImage"
      class="slider-arrow slider-arrow-right"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M9 5l7 7-7 7"
        />
      </svg>
    </button>

    <!-- Dots Indicator (shown when multiple images) -->
    <div
      v-if="images.length > 1"
      class="slider-dots"
    >
      <button
        v-for="(image, index) in images"
        :key="index"
        @click.stop="goToImage(index)"
        class="slider-dot"
        :class="{ 'slider-dot-active': currentIndex === index }"
        :aria-label="`Go to image ${index + 1}`"
      />
    </div>

    <!-- Logo at bottom right corner -->
    <div class="slider-logo">
      <img :src="LogoImage" alt="Logo" class="logo-image" />
    </div>
  </div>
</template>

<style>
.image-slider {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: var(--color-gray-200);
  border-radius: 12px 12px 0 0;
}

.slider-container {
  display: flex;
  height: 100%;
  transition: transform 0.5s ease-out;
}

.slider-slide {
  min-width: 100%;
  height: 100%;
  flex-shrink: 0;
}

.slider-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.slider-placeholder {
  width: 100%;
  height: 100%;
  background-color: var(--color-gray-200);
  display: flex;
  align-items: center;
  justify-content: center;
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

.slider-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
  width: 2rem;
  height: 2rem;
  border-radius: 9999px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(255, 255, 255, 0.9);
  transition: all var(--transition-base);
  cursor: pointer;
  box-shadow: var(--shadow-md);
  border: none;
}

.slider-arrow:hover {
  background-color: var(--color-white);
}

.slider-arrow svg {
  width: 1rem;
  height: 1rem;
  color: var(--color-gray-700);
}

.slider-arrow-left {
  left: 0.5rem;
}

.slider-arrow-right {
  right: 0.5rem;
}

.slider-dots {
  position: absolute;
  bottom: 0.75rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
  display: flex;
  align-items: center;
  gap: 3px;
}

.slider-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  border: none;
  background-color: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  padding: 0;
  transition: all 0.3s ease;
  flex-shrink: 0;
}

.slider-dot:hover {
  background-color: rgba(255, 255, 255, 0.8);
}

.slider-dot-active {
  background-color: rgba(255, 255, 255, 1);
  width: 6px;
  height: 6px;
}

.slider-logo {
  position: absolute;
  bottom: 0.75rem;
  right: 0.75rem;
  z-index: 10;
}

.logo-image {
  height: auto;
  max-height: 24px;
  width: auto;
  object-fit: contain;
}

@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}
</style>
