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
    coordinates: [40.7128, -74.0060], // New York, NY
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
    coordinates: [34.0522, -118.2437], // Los Angeles, CA
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
    coordinates: [41.8781, -87.6298], // Chicago, IL
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
    coordinates: [29.7604, -95.3698], // Houston, TX
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
    coordinates: [33.4484, -112.0740], // Phoenix, AZ
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
    coordinates: [30.2672, -97.7431], // Austin, TX
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

const handleFilterChange = (filters) => {
  // Filter properties based on selected filters
  // This can be expanded to actually filter the properties list
  console.log('Filter changed:', filters)
  // You can implement actual filtering logic here
}
</script>

<template>
  <div class="app-wrapper">
    <!-- Header -->
    <Header />

    <!-- Filter Bar -->
    <FilterBar @filter-change="handleFilterChange" />

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
