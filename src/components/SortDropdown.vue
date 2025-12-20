<script setup>
import { ref } from 'vue'

const props = defineProps({
  modelValue: {
    type: String,
    default: 'New Listing',
  },
})

const emit = defineEmits(['update:modelValue'])

const isOpen = ref(false)

const options = [
  'New Listing',
  'Price (Low to High)',
  'Price (High to Low)',
  'Bedrooms',
  'Bathrooms',
  'Square Feet',
  'Days on Market',
]

const selectOption = (option) => {
  emit('update:modelValue', option)
  isOpen.value = false
}

const toggleDropdown = () => {
  isOpen.value = !isOpen.value
}

const closeDropdown = () => {
  isOpen.value = false
}

const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeDropdown()
  } else if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault()
    toggleDropdown()
  }
}
</script>

<template>
  <div 
    class="sort-dropdown-wrapper" 
    :class="{ open: isOpen }" 
    @mouseleave="closeDropdown"
    @keydown="handleKeydown"
  >

      <span class="sort-label">Sort by: </span>
      <button
        type="button"
        class="sort-section"
        @click="toggleDropdown"
        :aria-expanded="isOpen"
        aria-haspopup="listbox"
        aria-label="Sort properties"
      >
        <span class="sort-value">{{ modelValue }}</span>
        <img class="sort-icon" alt="Dropdown indicator" src="../icons/path 3557.svg" />
      </button>

    <!-- Dropdown Menu -->
    <transition
      enter-active-class="fade-in-down"
      leave-active-class="fade-out-up"
    >
      <div
        v-if="isOpen"
        class="sort-menu"
        role="listbox"
      >
        <ul>
          <li
            v-for="option in options"
            :key="option"
            role="option"
            :aria-selected="option === modelValue"
            @click="selectOption(option)"
            class="sort-menu-item"
            :class="{ active: option === modelValue }"
          >
            {{ option }}
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<style>
.fade-in-down {
  animation: fadeInDown var(--transition-base);
}

.fade-out-up {
  animation: fadeOutUp var(--transition-base);
}

@keyframes fadeOutUp {
  0% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateY(-4px);
  }
}

.sort-section {
  background: none;
  border: none;
  padding: 0;
  margin: 0;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 4px;
  font: inherit;
  color: inherit;
}

.sort-section:focus {
  outline: 2px solid #0b5aa5;
  outline-offset: 2px;
  border-radius: 4px;
}

.sort-menu ul {
  list-style: none;
  padding: 0.25rem 0;
  margin: 0;
}
</style>
