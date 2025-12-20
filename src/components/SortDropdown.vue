<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const props = defineProps({
  modelValue: {
    type: String,
    default: 'New Listing',
  },
})

const emit = defineEmits(['update:modelValue'])

const isOpen = ref(false)
const dropdownRef = ref(null)

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

const handleClickOutside = (event) => {
  if (dropdownRef.value && !dropdownRef.value.contains(event.target)) {
    closeDropdown()
  }
}

const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeDropdown()
  } else if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault()
    toggleDropdown()
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>

<template>
  <div 
    ref="dropdownRef"
    class="sort-dropdown-wrapper" 
    :class="{ open: isOpen }" 
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
        @mouseenter.stop
        @mouseleave.stop
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
.sort-dropdown-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  gap: 4px;
  white-space: nowrap;
}

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

.sort-menu {
  top: calc(100% + 8px) !important;
  margin-top: 0 !important;
}

.sort-menu ul {
  list-style: none;
  padding: 0.25rem 0;
  margin: 0;
}
</style>
