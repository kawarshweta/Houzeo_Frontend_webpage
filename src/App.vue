<script setup>
import { ref, computed } from 'vue'
import Header from './components/Header.vue'
import FilterBar from './components/FilterBar.vue'
import MapSection from './components/MapSection.vue'
import PropertyList from './components/PropertyList.vue'
import SortDropdown from './components/SortDropdown.vue'

import image1 from './assets/1.png'
import image2 from './assets/2.png'
import image3 from './assets/3.png'
import image4 from './assets/4.png'

const properties = ref([
  {
    id: 1,
    type: 'House For Sale',
    price: 3349000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    mlsInfo: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    daysOnMarket: 6,
    isFavorite: false,
    images: [image1, image2, image3, image4],
    coordinates: [30.2672, -97.7431],
  },
  {
    id: 2,
    type: 'Condo For Sale',
    price: 3349000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    mlsInfo: "Sotheby's International Realty",
    daysOnMarket: 12,
    isFavorite: false,
    images: [image2, image3, image4, image1],
    coordinates: [32.7767, -96.7970],
  },
  {
    id: 3,
    type: 'Multi-family home For Sale',
    price: 3349000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    mlsInfo: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    daysOnMarket: 3,
    isFavorite: false,
    images: [image3, image4, image1, image2],
    coordinates: [29.7604, -95.3698],
  },
  {
    id: 4,
    type: 'House For Sale',
    price: 3349000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    mlsInfo: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    daysOnMarket: 10,
    isFavorite: false,
    images: [image4, image1, image2, image3],
    coordinates: [29.4241, -98.4936],
  },
  {
    id: 5,
    type: 'Townhouse For Sale',
    price: 3349000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    mlsInfo: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    daysOnMarket: 4,
    isFavorite: false,
    images: [image1, image3, image2, image4],
    coordinates: [32.7555, -97.3308],
  },
  {
    id: 6,
    type: 'Condo For Sale',
    price: 3349000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    mlsInfo: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    daysOnMarket: 8,
    isFavorite: false,
    images: [image2, image4, image1, image3],
    coordinates: [31.7619, -106.4850],
  },
])

const selectedSort = ref('New Listing')
const showMobileMap = ref(false)

const toggleFavorite = (propertyId) => {
  if (!propertyId) return
  const property = properties.value.find((p) => p?.id === propertyId)
  if (property) {
    property.isFavorite = !property.isFavorite
  }
}

const propertyCount = computed(() => {
  return new Intl.NumberFormat('en-US').format(properties.value.length)
})
</script>

<template>
  <div class="app-wrapper">
    <!-- Header -->
    <Header />

    <!-- Filter Bar -->
    <FilterBar />

    <!-- Main Content -->
    <main class="main-content">
      <!-- Mobile Map Toggle -->

      <!-- Mobile Map (Collapsible) -->
      <div
        v-if="showMobileMap"
        class="mobile-map-container animate-fade-in"
      >
        <MapSection :properties="properties" />
      </div>

      <div class="content-layout">
        <!-- Map Section (Desktop) -->
        <div class="map-section-desktop">
          <MapSection :properties="properties" />
        </div>

        <!-- Property Listings Section -->
        <div class="property-list-section">
          <!-- Results Header -->
          <div class="results-header">
            <h1 class="location-title">Austin, TX real estate & homes for sale</h1>
            <div class="results-info">
              <div class="results-count">{{ propertyCount }} Homes</div>
              <SortDropdown v-model="selectedSort" />
            </div>
          </div>

          <!-- Property List -->
          <PropertyList :properties="properties" @toggle-favorite="toggleFavorite" />
          
        </div>
      </div>
    </main>
  </div>
</template>

<style>

</style>
