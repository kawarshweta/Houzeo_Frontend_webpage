<script setup>
import { ref, computed } from 'vue'
import ImageSlider from './ImageSlider.vue'
import ViewsIcon from '../icons/views-icon.svg'
import dotimage from '../icons/dot.svg'

const props = defineProps({
  property: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['toggle-favorite'])

const isHovered = ref(false)

const formattedPrice = computed(() => {
  const price = props.property?.price ?? 0
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    maximumFractionDigits: 0,
  }).format(price)
})

const addressParts = computed(() => {
  const address = props.property?.address || ''
  if (!address) {
    return { street: '', cityStateZip: '' }
  }
  const lastCommaIndex = address.lastIndexOf(',')
  if (lastCommaIndex === -1) {
    return { street: address, cityStateZip: '' }
  }
  let cityStateZip = address.substring(lastCommaIndex + 1).trim()
  // Ensure there's a space after commas in city/state/zip part
  cityStateZip = cityStateZip.replace(/,(?=\S)/g, ', ')
  return {
    street: address.substring(0, lastCommaIndex + 1).trim(),
    cityStateZip: cityStateZip
  }
})

const handleFavoriteClick = (event) => {
  event.preventDefault()
  emit('toggle-favorite', props.property.id)
}
</script>

<template>
  <article
    class="property-card"
    :class="{ 'card-hover': isHovered }"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
  >
    <!-- Image Slider Section -->
    <div class="property-image-container">
      <ImageSlider :images="property.images" :is-hovered="isHovered" />

      <!-- Days on Houzeo Badge (Top Left) -->
      <div class="days-badge-top" v-if="property.daysOnMarket !== undefined">
        {{ property.daysOnMarket }} days on Houzeo
      </div>

      <!-- Favorite Button (Top Right) -->
      <button
        @click.stop="handleFavoriteClick"
        class="favorite-btn"
        :class="{ active: property.isFavorite }"
      >
        <svg 
          width="22" 
          height="20" 
          viewBox="0 0 22 20" 
          fill="none" 
          xmlns="http://www.w3.org/2000/svg"
          class="heart-icon-svg"
        >
          <path 
            d="M6 1C3.239 1 1 3.216 1 5.95C1 8.157 1.875 13.395 10.488 18.69C10.6423 18.7839 10.8194 18.8335 11 18.8335C11.1806 18.8335 11.3577 18.7839 11.512 18.69C20.125 13.395 21 8.157 21 5.95C21 3.216 18.761 1 16 1C13.239 1 11 4 11 4C11 4 8.761 1 6 1Z" 
            :fill="property.isFavorite ? '#ef4444' : '#222222'"
            :fill-opacity="property.isFavorite ? '1' : '0.7'"
            stroke="white" 
            stroke-width="2" 
            stroke-linecap="round" 
            stroke-linejoin="round"
          />
        </svg>
      </button>
    </div>

    <!-- Property Details -->
    <div class="property-details">
      <!-- Views Only (Property Type Removed) -->
      <div class="property-header-info">
        <div class="badge" v-if="property.daysOnMarket !== undefined">
          <img :src="dotimage" alt="Days indicator" class="dot-img" /> 
          {{ property.daysOnMarket }} days on Houzeo
        </div>
        <div class="property-views">
          <img :src="ViewsIcon" alt="Views" class="views-icon" />
          <span>2.3K</span>
        </div>
      </div>

      <div class='pricing-section'>
      <!-- Price -->
      <div class="property-price-wrapper">
        <h3 class="property-price">{{ formattedPrice }}</h3>
      </div>

      <!-- Property Stats -->
      <div class="property-stats">
        <div class="stat-item">
          <div class="stat-number">{{ property.bedrooms }}</div>
          <div class="stat-label">Beds</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">{{ property.bathrooms }}</div>
          <div class="stat-label">Baths</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">{{ property.sqft }}</div>
          <div class="stat-label">sqft.</div>
        </div>
      </div>
    </div>

      <!-- Address -->
      <p class="property-address ">
        {{ addressParts.street }}<span class="address-city-state">{{ addressParts.cityStateZip }}</span>
      </p>

      <!-- MLS Info -->
      <p class="property-mls" v-if="property.mlsInfo">
        {{ property.mlsInfo }}
      </p>
    </div>
  </article>
</template>

<style>
.property-card {
  border-radius: 16px;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.1);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: all 0.3s ease;
  width: 100%;
  box-sizing: border-box;
}


.property-image-container {
  position: relative;
  width: 100%;
  height: 192px;
  overflow: hidden;
}


.days-badge-top {
  position: absolute;
  top: 16px;
  left: 16px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.15);
  border-radius: 24px;
  background-color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 4px 8px;
  font-size: 12px;
  font-weight: 500;
  z-index: 2;
}

.favorite-btn {
  position: absolute;
  top: 15.96px;
  right: 16px;
  width: 24px;
  height: 24px;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 2;
  transition: transform 0.3s ease;
}

.favorite-btn:hover {
  transform: scale(1.2);
  animation: pulseHeart 0.6s ease-in-out;
}

.heart-icon-svg {
  width: 100%;
  height: 100%;
  transition: all 0.3s ease;
}

.property-details {
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 8px;
  width: 100%;
  max-width: 100%;
  min-width: 0;
  box-sizing: border-box;
}

.property-header-info {
  width: 100%;
  max-width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  min-width: 0;
}

.property-views {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 3px;
  opacity: 0.7;
  font-size: 12px;
}

.views-icon {
  width: 16px;
  height: 12px;
}

.property-price-wrapper {
  width: 100%;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 20px;
}

.property-price {
  font-size: 18px;
  font-weight: 600;
  color: #0b5aa5;
  line-height: 1;
}
.pricing-section{
  display: flex;
}
.property-stats {
  width: 100%;
  max-width: 173px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  font-size: 14px;
}

.stat-item {
  display: flex;
  align-items: center;
  gap: 4px;
}

.stat-number {
  font-size: 14px;
  font-weight: 600;
  color: #0b5aa5;
}

.stat-label {
  font-size: 12px;
  color: rgba(0, 0, 0, 0.5);
  line-height: 1;
}
.badge{
      box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.15);
    border-radius: 24px;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 4px 8px;
    font-size: 12px;
    font-weight: 500;
    z-index: 2;
    align-items: center;
    gap: 6px;
}
.property-address {
  width: 100%;
  font-size: 12px;
  font-weight: 500;
  color: #000;
  line-height: 1.4;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.property-address .address-city-state {
  font-weight: normal;
  color: rgba(0, 0, 0, 0.7);
}

.property-mls {
  width: 100%;
  font-size: 12px;
  color: rgba(0, 0, 0, 0.5);
  line-height: 1.4;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

@keyframes pulseHeart {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.3);
  }
}
</style>
