<script setup>
import { onMounted, onBeforeUnmount, watch, ref } from 'vue'
import L from 'leaflet'

const props = defineProps({
  properties: {
    type: Array,
    required: true,
  },
})

const mapContainer = ref(null)
let map = null
let markers = []

// Fix for default marker icon issue in Leaflet with webpack/vite
delete L.Icon.Default.prototype._getIconUrl
L.Icon.Default.mergeOptions({
  iconRetinaUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-icon-2x.png',
  iconUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-icon.png',
  shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-shadow.png',
})

const initializeMap = () => {
  if (!mapContainer.value) return

  // Default to USA center view - show full United States map
  const defaultCenter = [39.8283, -98.5795] // Geographic center of United States
  let center = defaultCenter
  let zoom = 4 // Zoom level 4 shows the entire USA

  if (props.properties && props.properties.length > 0) {
    const validCoords = props.properties.filter(p => p.coordinates && p.coordinates.length === 2)
    if (validCoords.length > 0) {
      // If properties exist, we can still show USA but zoom to properties if they're close together
      const avgLat = validCoords.reduce((sum, p) => sum + p.coordinates[0], 0) / validCoords.length
      const avgLng = validCoords.reduce((sum, p) => sum + p.coordinates[1], 0) / validCoords.length
      
      // For single property, zoom in more; for multiple, keep wider USA view
      if (validCoords.length === 1) {
        center = [avgLat, avgLng]
        zoom = 10
      } else {
        // Keep USA view but center on properties
        center = [avgLat, avgLng]
        zoom = 5 // Still show wider USA context
      }
    }
  }

  // Initialize map
  map = L.map(mapContainer.value, {
    center,
    zoom,
    zoomControl: true,
    attributionControl: true,
    keyboard: true,
    scrollWheelZoom: true,
    doubleClickZoom: true,
    boxZoom: true,
    dragging: true,
  })

  // Add tile layer
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
    maxZoom: 19,
  }).addTo(map)

  // Add markers for properties
  updateMarkers()
}

const updateMarkers = () => {
  if (!map) return

  // Clear existing markers
  markers.forEach(marker => map.removeLayer(marker))
  markers = []

  // Add markers for each property
  if (props.properties && props.properties.length > 0) {
    props.properties.forEach(property => {
      if (property.coordinates && property.coordinates.length === 2) {
        const [lat, lng] = property.coordinates
        
        // Create custom marker icon
        const markerIcon = L.divIcon({
          className: 'custom-marker',
          html: `
            <div class="marker-pin">
              <div class="marker-content">
                <span class="marker-price">$${(property.price / 1000).toFixed(0)}k</span>
              </div>
            </div>
          `,
          iconSize: [60, 72],
          iconAnchor: [30, 34],
          popupAnchor: [0, -34],
        })

        const marker = L.marker([lat, lng], { icon: markerIcon })
          .addTo(map)
          .bindPopup(`
            <div class="map-popup">
              <strong>${property.type}</strong><br>
              <span>$${property.price.toLocaleString()}</span><br>
              <small>${property.address}</small>
            </div>
          `)

        markers.push(marker)
      }
    })

    // Fit map to show all markers, but maintain USA context
    if (markers.length > 1) {
      const group = new L.featureGroup(markers)
      const bounds = group.getBounds()
      const latDiff = bounds.getNorth() - bounds.getSouth()
      const lngDiff = bounds.getEast() - bounds.getWest()
      
      // If markers are spread across USA, show full USA view
      // If markers are close together, zoom to them
      if (latDiff > 10 || lngDiff > 15) {
        // Markers are spread out - show USA map
        map.setView([39.8283, -98.5795], 4)
      } else {
        // Markers are close together - fit to them
        map.fitBounds(bounds.pad(0.2))
      }
    } else if (markers.length === 1) {
      const [lat, lng] = props.properties[0].coordinates
      map.setView([lat, lng], 10)
    }
  } else {
    // No properties - show full USA map
    map.setView([39.8283, -98.5795], 4)
  }
}

onMounted(() => {
  // Small delay to ensure DOM is ready
  setTimeout(() => {
    initializeMap()
  }, 100)
})

onBeforeUnmount(() => {
  if (map) {
    map.remove()
    map = null
  }
  markers = []
})

// Watch for property changes
watch(() => props.properties, () => {
  if (map) {
    updateMarkers()
  }
}, { deep: true })
</script>

<template>
  <div 
    ref="mapContainer" 
    class="map-container"
    tabindex="0"
    aria-label="Map"
    aria-roledescription="map"
    role="region"
  ></div>
</template>

<style>
.map-container {
  width: 100%;
  height: 100%;
  border-radius: 0;
  overflow: hidden;
  background-color: #f3f4f6;
  position: relative;
  outline: none;
}

.map-container:focus {
  outline: 2px solid #3b82f6;
  outline-offset: -2px;
}

/* Custom marker styles */
.custom-marker {
  background: transparent;
  border: none;
}

.marker-pin {
  position: relative;
  width: 60px;
  height: 72px;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding-top: 0;
}

.marker-content {
  background: #ffffff;
  border: 2px solid #1a73e8;
  border-radius: 6px;
  padding: 6px 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.12);
  font-weight: 600;
  font-size: 12px;
  color: #1f2937;
  white-space: nowrap;
  position: relative;
  margin-top: 0;
  z-index: 1;
}

.marker-content::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 6px solid #1a73e8;
  z-index: 0;
}

.marker-price {
  color: #1f2937;
  font-weight: 600;
}

/* Popup styles */
.map-popup {
  font-family: inherit;
  min-width: 200px;
}

.map-popup strong {
  display: block;
  margin-bottom: 4px;
  color: #1f2937;
  font-size: 14px;
}

.map-popup span {
  display: block;
  color: #3b82f6;
  font-weight: 600;
  font-size: 16px;
  margin-bottom: 4px;
}

.map-popup small {
  color: #6b7280;
  font-size: 12px;
}

/* Leaflet popup customization */
.leaflet-popup-content-wrapper {
  border-radius: 8px;
  padding: 0;
  position: relative;
  overflow: visible;
}

.leaflet-popup-content {
  margin: 12px;
  margin-right: 32px;
  font-size: 14px;
  padding-right: 8px;
}

.leaflet-popup-tip {
  background: white;
}

/* Close button styling - keep it inside the popup */
.leaflet-popup-close-button {
  position: absolute;
  top: 8px;
  right: 8px;
  width: 24px;
  height: 24px;
  padding: 0;
  margin: 0;
  text-align: center;
  line-height: 24px;
  font-size: 18px;
  font-weight: 300;
  color: #6b7280;
  background: transparent;
  border: none;
  cursor: pointer;
  z-index: 10;
  transition: color 0.2s ease;
}

.leaflet-popup-close-button:hover {
  color: #1f2937;
  background: rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.leaflet-popup-close-button:active {
  color: #000;
}

/* Ensure popup container has proper positioning */
.leaflet-popup {
  margin-bottom: 0;
}

.leaflet-popup-content-wrapper {
  position: relative;
  overflow: hidden;
}
</style>
