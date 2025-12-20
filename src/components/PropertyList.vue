<script setup>
import PropertyCard from './PropertyCard.vue'

defineProps({
  properties: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['toggle-favorite'])

const handleToggleFavorite = (propertyId) => {
  if (propertyId) {
    emit('toggle-favorite', propertyId)
  }
}
</script>

<template>
  <div class="property-grid">
    <PropertyCard
      v-for="property in properties"
      :key="property.id"
      :property="property"
      class="property-card-item"
      @toggle-favorite="handleToggleFavorite"
    />
  </div>
</template>
