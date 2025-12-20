<template>
  <div class="filter-bar-wrapper">
    <!-- First Row: Search Bar + Filter Button (Mobile) -->
    <div class="search-row">
      <div class="navigation">
        <div class="frame2">
          <div class="city-neighborhood-address">{{ displayLocation }}</div>
        </div>
        <div class="frame3">
          <button
            v-if="location"
            type="button"
            class="basilcross-solid-icon"
            aria-label="Clear location"
            @click="clearLocation"
          >
            <img 
              alt="Clear" 
              src="../icons/basil_cross-solid.svg"
            />
          </button>
          <img class="group-icon" alt="Search" src="../icons/Group-1.svg" />
        </div>
      </div>
      <div class="filter-button-mobile">
        <img class="vector-icon" alt="Filter" src="../icons/filter.svg" />
        <span class="filter-badge">2</span>
      </div>
    </div>
    
    <!-- Second Row: Filter Buttons -->
    <div class="filters-row">
      <div class="frame4">
        <div class="product">For Sale</div>
        <img class="frame-icon" alt="Dropdown indicator" src="../icons/path 3557.svg" />
      </div>
      <div class="frame5">
        <div class="product2">Price</div>
        <img class="frame-icon" alt="Dropdown indicator" src="../icons/path 3557.svg" />
      </div>
      <div class="save-search-button">
        <div class="save-search-text">Save Search</div>
      </div>
    </div>
    
    <!-- Desktop Only Filters -->
    <div class="desktop-filters">
      <div class="frame6">
        <div class="product2">Beds & Baths</div>
        <img class="frame-icon" alt="Dropdown indicator" src="../icons/path 3557.svg" />
      </div>
      <div class="frame7">
        <div class="product2">Property Type</div>
        <img class="frame-icon" alt="Dropdown indicator" src="../icons/path 3557.svg" />
      </div>
      <div class="frame7 filter-button-desktop">
        <img class="vector-icon" alt="Filter icon" src="../icons/filter.svg" />
        <div class="product2">Filters</div>
      </div>
      <div class="frame9">
        <img class="vector-icon2" alt="Saved icon" src="../icons/saved.svg" />
        <div class="city-neighborhood-address">Saved</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  location: {
    type: String,
    default: 'Austin, TX'
  }
})

const emit = defineEmits(['update:location'])

const displayLocation = computed(() => props.location || 'Austin, TX')

const clearLocation = () => {
  emit('update:location', '')
}
</script>

<style>
.filter-bar-wrapper {
  width: 100%;
  position: relative;
  box-shadow: 0px 2px 10px rgba(152, 152, 152, 0.2);
  background-color: #fff;
  display: flex;
  align-items: center;
  align-content: flex-start;
  padding: 16px 24px;
  box-sizing: border-box;
  gap: 16px;
  row-gap: 16px;
  text-align: left;
  font-size: 14px;
  color: #000;
  flex-wrap: wrap;
  margin: 0;
  border: none;
  line-height: 1;
  overflow: hidden;
  height: fit-content;
  min-height: fit-content;
}

.search-row {
  display: flex;
  align-items: center;
  gap: 12px;
  width: 100%;
  order: 1;
}

.filters-row {
  display: flex;
  align-items: center;
  gap: 12px;
  width: 100%;
  order: 2;
  flex-wrap: wrap;
}

.desktop-filters {
  display: flex;
  align-items: center;
  gap: 16px;
  order: 3;
}

.filter-button-mobile {
  display: none;
  position: relative;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  flex-shrink: 0;
}

.filter-button-mobile:hover {
  border-color: #0b5aa5;
  background-color: #f3f7fa;
}

.filter-button-mobile .vector-icon {
  height: 18px;
  width: 16px;
  position: relative;
  flex-shrink: 0;
}

.filter-badge {
  position: absolute;
  top: -2px;
  right: -2px;
  background-color: #2876c1;
  color: #fff;
  border-radius: 50%;
  width: 18px;
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 10px;
  font-weight: 600;
  line-height: 1;
}

.save-search-button {
  height: 48px;
  border-radius: 8px;
  background: linear-gradient(90deg, #2876C1 0%, #0E5293 100%);
  border: none;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 14px 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  margin: 0;
  border-radius: 25px;
}

.save-search-button:hover {
  opacity: 0.9;
}

.save-search-text {
  color: #fff;
  font-size: 14px;
  font-weight: 500;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.navigation {
  flex: 1;
  min-width: 0;
  max-width: 402px;
  border-radius: 500px;
  background-color: #f3f7fa;
  border: 2px solid #2876c1;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 8px 8px 16px;
  gap: 20px;
  flex-shrink: 1;
  margin: 0;
}

.frame2 {
  display: flex;
  align-items: center;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.city-neighborhood-address {
  position: relative;
  font-weight: 500;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.frame3 {
  width: 72px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.basilcross-solid-icon {
  height: 32px;
  width: 32px;
  position: relative;
  box-shadow: 0px 4px 4px rgba(255, 255, 255, 0.1);
  border-radius: 50px;
  cursor: pointer;
  transition: opacity 0.2s ease;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: none;
  border: none;
  box-sizing: border-box;
}

.basilcross-solid-icon:hover {
  opacity: 0.7;
}

.basilcross-solid-icon img {
  width: 100%;
  height: 100%;
  display: block;
}

.group-icon {
  height: 32px;
  width: 32px;
  position: relative;
  cursor: pointer;
  transition: opacity 0.2s ease;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  display: block;
  box-sizing: border-box;
}

.group-icon:hover {
  opacity: 0.7;
}

.frame4 {
  height: 48px;
  border-radius: 8px;
  background-color: #f3f7fa;
  border: 1px solid #0b5aa5;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  padding: 14px 16px;
  gap: 12px;
  color: #0b5aa5;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  margin: 0;
  width: auto;
}

.frame4:hover {
  background-color: #e8f0f8;
}

.product {
  position: relative;
  font-weight: 600;
  display: inline-block;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.frame-icon {
  width: 11px;
    height: 5px;
  position: relative;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  display: block;
  box-sizing: border-box;
}

.frame5 {
  height: 48px;
  width: 154px;
  border-radius: 8px;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 16px;
  gap: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  margin: 0;
}

.frame5:hover {
  border-color: #0b5aa5;
  background-color: #f3f7fa;
}

.product2 {
  position: relative;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.frame6 {
  height: 48px;
  width: 184px;
  border-radius: 8px;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 16px;
  gap: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  margin: 0;
}

.frame6:hover {
  border-color: #0b5aa5;
  background-color: #f3f7fa;
}

.frame7 {
  height: 48px;
  border-radius: 8px;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  display: flex;
  align-items: center;
  padding: 14px 16px;
  gap: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  margin: 0;
}

.frame7:hover {
  border-color: #0b5aa5;
  background-color: #f3f7fa;
}

.vector-icon {
  height: 18px;
  width: 16px;
  position: relative;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  display: block;
  box-sizing: border-box;
}

.frame9 {
  height: 48px;
  width: 124px;
  border-radius: 500px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 14px 16px;
  gap: 16px;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  margin: 0;
}

.frame9:hover {
  border-color: #0b5aa5;
  background-color: #f3f7fa;
}

.vector-icon2 {
  height: 12px;
  width: 12px;
  position: relative;
  flex-shrink: 0;
  margin: 0;
  padding: 0;
  display: block;
  box-sizing: border-box;
}

/* Tablet styles */
@media (max-width: 1024px) {
  .filter-bar-wrapper {
    padding: 16px 20px;
    gap: 12px;
    flex-wrap: wrap;
  }

  .search-row {
    width: 100%;
  }

  .filters-row {
    width: 100%;
  }

  .navigation {
    flex: 1;
    min-width: 0;
  }

  .frame4 {
    width: auto;
    min-width: 100px;
  }

  .frame5 {
    width: auto;
    min-width: 100px;
  }

  .save-search-button {
    width: auto;
    min-width: 120px;
  }
}

/* Mobile styles */
@media (max-width: 768px) {
  .filter-bar-wrapper {
    padding: 12px 16px;
    gap: 12px;
    flex-direction: column;
    align-items: stretch;
  }

  .search-row {
    display: flex;
    width: 100%;
    gap: 12px;
    margin-bottom: 12px;
  }

  .navigation {
    flex: 1;
    min-width: 0;
    max-width: none;
  }

  .filter-button-mobile {
    display: flex;
  }

  .filters-row {
    display: flex;
    width: 100%;
    gap: 12px;
    flex-wrap: nowrap;
  }

  .frame4 {
    width: auto;
    flex: 0 0 auto;
    min-width: 100px;
  }

  .frame5 {
    width: auto;
    flex: 0 0 auto;
    min-width: 100px;
  }

  .save-search-button {
    width: auto;
    flex: 0 0 auto;
    min-width: 120px;
    margin-left: auto;
  }

  .desktop-filters {
    display: none;
  }
}

/* Small mobile styles */
@media (max-width: 480px) {
  .filter-bar-wrapper {
    padding: 12px;
    gap: 10px;
  }

  .search-row {
    gap: 10px;
    margin-bottom: 10px;
  }

  .navigation {
    padding: 8px 8px 8px 14px;
    gap: 12px;
  }

  .frame3 {
    width: auto;
    gap: 6px;
  }

  .filter-button-mobile {
    width: 44px;
    height: 44px;
  }

  .filters-row {
    gap: 10px;
  }

  .frame4 {
    height: 44px;
    padding: 12px 14px;
    min-width: 90px;
  }

  .frame5 {
    height: 44px;
    padding: 12px 14px;
    min-width: 80px;
  }

  .save-search-button {
    height: 44px;
    padding: 12px 16px;
    min-width: 110px;
  }

  .city-neighborhood-address {
    font-size: 13px;
  }

  .product,
  .product2,
  .save-search-text {
    font-size: 13px;
  }

  .basilcross-solid-icon,
  .group-icon {
    height: 28px;
    width: 28px;
  }
}

/* Extra small screens */
@media (max-width: 360px) {
  .filter-bar-wrapper {
    padding: 10px;
    gap: 8px;
  }

  .search-row {
    gap: 8px;
    margin-bottom: 8px;
  }

  .navigation {
    padding: 6px 6px 6px 12px;
    gap: 10px;
  }

  .filter-button-mobile {
    width: 40px;
    height: 40px;
  }

  .filters-row {
    gap: 6px;
  }

  .frame4,
  .frame5 {
    padding: 10px 12px;
    height: 40px;
    font-size: 12px;
    min-width: 70px;
  }

  .save-search-button {
    padding: 10px 14px;
    height: 40px;
    min-width: 100px;
  }

  .product,
  .product2,
  .save-search-text {
    font-size: 12px;
  }

  .city-neighborhood-address {
    font-size: 12px;
  }

  .basilcross-solid-icon,
  .group-icon {
    height: 24px;
    width: 24px;
  }
}

/* Desktop: Show all filters */
@media (min-width: 769px) {
  .filter-bar-wrapper {
    flex-direction: row;
    align-items: center;
  }

  .filter-button-mobile {
    display: none;
  }

  .save-search-button {
    display: none;
  }

  .desktop-filters {
    display: flex;
  }

  .search-row {
    width: auto;
    flex: 1 1 auto;
    min-width: 450px;
    order: 1;
  }

  .navigation {
    max-width: 600px;
    flex: 1;
  }

  .filters-row {
    width: auto;
    flex: 0 0 auto;
    order: 2;
  }

  .desktop-filters {
    order: 3;
  }
}
</style>
