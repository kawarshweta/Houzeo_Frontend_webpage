<template>
  <div class="header-wrapper">
    <!-- Mobile Menu Button -->
    <button 
      class="mobile-menu-button" 
      @click="toggleMobileMenu"
      aria-label="Toggle menu"
    >
      <svg 
        v-if="!isMobileMenuOpen" 
        class="menu-icon" 
        xmlns="http://www.w3.org/2000/svg" 
        width="26" 
        height="18" 
        viewBox="0 0 26 18" 
        fill="none"
      >
        <path d="M1.09865 17.0515C0.955976 17.0559 0.813881 17.0315 0.680789 16.98C0.547697 16.9284 0.42632 16.8506 0.323856 16.7512C0.221392 16.6519 0.139928 16.5329 0.0842967 16.4015C0.0286655 16.27 0 16.1287 0 15.986C0 15.8433 0.0286655 15.702 0.0842967 15.5705C0.139928 15.4391 0.221392 15.3201 0.323856 15.2208C0.42632 15.1214 0.547697 15.0436 0.680789 14.992C0.813881 14.9405 0.955976 14.9161 1.09865 14.9205H24.5446C24.6873 14.9161 24.8294 14.9405 24.9625 14.992C25.0956 15.0436 25.217 15.1214 25.3194 15.2208C25.4219 15.3201 25.5034 15.4391 25.559 15.5705C25.6146 15.702 25.6433 15.8433 25.6433 15.986C25.6433 16.1287 25.6146 16.27 25.559 16.4015C25.5034 16.5329 25.4219 16.6519 25.3194 16.7512C25.217 16.8506 25.0956 16.9284 24.9625 16.98C24.8294 17.0315 24.6873 17.0559 24.5446 17.0515H1.09865ZM1.09865 9.5915C0.955976 9.59587 0.813881 9.57154 0.680789 9.51997C0.547697 9.46839 0.42632 9.3906 0.323856 9.29123C0.221392 9.19186 0.139928 9.07292 0.0842967 8.94147C0.0286655 8.81002 0 8.66874 0 8.526C0 8.38326 0.0286655 8.24198 0.0842967 8.11053C0.139928 7.97908 0.221392 7.86014 0.323856 7.76077C0.42632 7.6614 0.547697 7.58361 0.680789 7.53203C0.813881 7.48045 0.955976 7.45613 1.09865 7.4605H24.5446C24.6873 7.45613 24.8294 7.48045 24.9625 7.53203C25.0956 7.58361 25.217 7.6614 25.3194 7.76077C25.4219 7.86014 25.5034 7.97908 25.559 8.11053C25.6146 8.24198 25.6433 8.38326 25.6433 8.526C25.6433 8.66874 25.6146 8.81002 25.559 8.94147C25.5034 9.07292 25.4219 9.19186 25.3194 9.29123C25.217 9.3906 25.0956 9.46839 24.9625 9.51997C24.8294 9.57154 24.6873 9.59587 24.5446 9.5915H1.09865ZM1.09865 2.1315C0.955976 2.13587 0.813881 2.11154 0.680789 2.05997C0.547697 2.00839 0.42632 1.9306 0.323856 1.83123C0.221392 1.73186 0.139928 1.61292 0.0842967 1.48147C0.0286655 1.35002 0 1.20874 0 1.066C0 0.923262 0.0286655 0.78198 0.0842967 0.65053C0.139928 0.519081 0.221392 0.400142 0.323856 0.300769C0.42632 0.201396 0.547697 0.123613 0.680789 0.0720332C0.813881 0.0204537 0.955976 -0.00387122 1.09865 0.000500042H17.6106C17.7533 -0.00387122 17.8954 0.0204537 18.0285 0.0720332C18.1616 0.123613 18.283 0.201396 18.3854 0.300769C18.4879 0.400142 18.5694 0.519081 18.625 0.65053C18.6806 0.78198 18.7093 0.923262 18.7093 1.066C18.7093 1.20874 18.6806 1.35002 18.625 1.48147C18.5694 1.61292 18.4879 1.73186 18.3854 1.83123C18.283 1.9306 18.1616 2.00839 18.0285 2.05997C17.8954 2.11154 17.7533 2.13587 17.6106 2.1315H1.09865Z" fill="black"/>
      </svg>
      <svg 
        v-else 
        class="menu-icon" 
        width="27.4" 
        height="27.4" 
        viewBox="0 0 27.4 27.4" 
        fill="none"
      >
        <path d="M1 1L26.4 26.4M26.4 1L1 26.4" stroke="black" stroke-width="2" stroke-linecap="round"/>
      </svg>
    </button>

    <!-- Logo -->
    <img class="header-logo" alt="Houzeo Logo" :src="GroupIcon" loading="eager" />

    <!-- Desktop Navigation -->
    <div class="desktop-navigation">
      <div class="group2">
          <div class="group5">
          <div class="product">Product</div>
          <img class="path-3557-icon" alt="Dropdown indicator" :src="Path3557Icon" />
        </div>
        <div class="how-houzeo-works">How Houzeo Works</div>
        <div class="reviews">Reviews</div>
                <div class="group4">
          <div class="buy">Buy</div>
          <img class="path-3451-icon" alt="Dropdown indicator" :src="Path3451Icon" />
        </div>
        <div class="group3">
          <div class="sell">Sell</div>
          <img class="path-3450-icon" alt="Dropdown indicator" :src="Path3450Icon" />
        </div>
        <div class="pricing">Pricing</div>
        <div class="group6">
          <div class="resources">Resources</div>
          <img class="path-3452-icon" alt="Dropdown indicator" :src="Path3452Icon" />
        </div>
        <div class="sign-in">Sign In</div>
              <div class="am-to-6pm-cst-mon-sat">
        <div class="div">(844) 448-0110</div>
        <div class="am-to-6pm">(9am to 6pm CST, Mon-Sat)</div>
      </div>
            <div class="group">
        <div class="start-free-listing">Start Free Listing</div>
      </div>
      </div>
    </div>



    <!-- Mobile Action Button -->
    <button class="mobile-action-button" aria-label="Start Free Listing">
      <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 28 28" fill="none">
        <path d="M13.7221 16.168C12.565 16.168 11.434 15.8249 10.472 15.1821C9.50994 14.5393 8.76014 13.6256 8.31737 12.5567C7.8746 11.4878 7.75876 10.3115 7.98448 9.17672C8.21021 8.04193 8.76736 6.99956 9.5855 6.18142C10.4036 5.36329 11.446 4.80613 12.5808 4.58041C13.7156 4.35469 14.8918 4.47054 15.9608 4.91331C17.0297 5.35608 17.9434 6.10589 18.5862 7.06791C19.229 8.02994 19.5721 9.16098 19.5721 10.318C19.5705 11.869 18.9536 13.3561 17.8569 14.4528C16.7601 15.5496 15.2731 16.1664 13.7221 16.168ZM13.7221 5.886C12.8455 5.886 11.9886 6.14594 11.2598 6.63293C10.5309 7.11993 9.96287 7.8121 9.62743 8.62194C9.29198 9.43179 9.20422 10.3229 9.37523 11.1826C9.54624 12.0424 9.96835 12.8321 10.5882 13.4519C11.208 14.0717 11.9977 14.4938 12.8574 14.6648C13.7172 14.8358 14.6083 14.7481 15.4181 14.4126C16.2279 14.0772 16.9202 13.5091 17.4072 12.7803C17.8941 12.0514 18.1541 11.1946 18.1541 10.318C18.1538 9.14265 17.6868 8.0155 16.8557 7.1844C16.0246 6.3533 14.8974 5.88626 13.7221 5.886Z" fill="#020202"/>
        <path d="M13.721 27.442C11.0072 27.442 8.35442 26.6373 6.09802 25.1296C3.84161 23.6219 2.08297 21.479 1.04446 18.9718C0.00594795 16.4646 -0.265777 13.7058 0.26365 11.0442C0.793078 8.38256 2.09988 5.93771 4.01879 4.0188C5.93771 2.09988 8.38255 0.793079 11.0442 0.263651C13.7058 -0.265776 16.4646 0.00594509 18.9718 1.04446C21.479 2.08296 23.6219 3.84162 25.1296 6.09803C26.6373 8.35443 27.442 11.0072 27.442 13.721C27.4393 17.3592 25.9929 20.8477 23.4203 23.4203C20.8477 25.9929 17.3592 27.4394 13.721 27.442ZM13.721 1.421C11.2883 1.421 8.91022 2.14239 6.88749 3.49393C4.86477 4.84547 3.28824 6.76647 2.35728 9.014C1.42632 11.2615 1.18274 13.7347 1.65734 16.1206C2.13194 18.5066 3.3034 20.6982 5.02358 22.4184C6.74377 24.1386 8.93542 25.3101 11.3214 25.7847C13.7074 26.2593 16.1805 26.0157 18.428 25.0847C20.6755 24.1538 22.5965 22.5772 23.9481 20.5545C25.2996 18.5318 26.021 16.1537 26.021 13.721C26.0126 10.4614 24.714 7.3378 22.4091 5.03293C20.1042 2.72806 16.9806 1.42945 13.721 1.421Z" fill="#020202"/>
        <path d="M5.10701 23.292L3.93701 22.512C4.99549 20.8972 6.43714 19.5695 8.13341 18.6472C9.82967 17.7249 11.7278 17.2368 13.6586 17.2263C15.5893 17.2158 17.4926 17.6833 19.1988 18.587C20.905 19.4908 22.361 20.8028 23.437 22.406L22.267 23.186C21.3165 21.7795 20.0334 20.6294 18.5318 19.8377C17.0301 19.0461 15.3562 18.6374 13.6586 18.6479C11.9611 18.6583 10.2924 19.0877 8.80061 19.8979C7.30883 20.708 6.0401 21.8739 5.10701 23.292Z" fill="#020202"/>
      </svg>
    </button>

    <!-- Mobile Menu Overlay -->
    <div 
      v-if="isMobileMenuOpen" 
      class="mobile-menu-overlay" 
      @click="closeMobileMenu"
    ></div>

    <!-- Mobile Menu -->
    <div 
      class="mobile-menu" 
      :class="{ 'mobile-menu-open': isMobileMenuOpen }"
    >
      <div class="mobile-menu-content">
        <div class="mobile-menu-item" @click="closeMobileMenu">How Houzeo Works</div>
        <div class="mobile-menu-item dropdown-item" @click="closeMobileMenu">
          <span>Product</span>
          <img class="dropdown-icon" alt="Dropdown indicator" :src="Path3557Icon" />
        </div>
        <div class="mobile-menu-item dropdown-item" @click="closeMobileMenu">
          <span>Resources</span>
          <img class="dropdown-icon" alt="Dropdown indicator" :src="Path3452Icon" />
        </div>
        <div class="mobile-menu-item dropdown-item" @click="closeMobileMenu">
          <span>Buy</span>
          <img class="dropdown-icon" alt="Dropdown indicator" :src="Path3451Icon" />
        </div>
        <div class="mobile-menu-item dropdown-item" @click="closeMobileMenu">
          <span>Sell</span>
          <img class="dropdown-icon" alt="Dropdown indicator" :src="Path3450Icon" />
        </div>
        <div class="mobile-menu-item" @click="closeMobileMenu">Reviews</div>
        <div class="mobile-menu-item" @click="closeMobileMenu">Pricing</div>
        <div class="mobile-menu-item" @click="closeMobileMenu">Sign In</div>
        <div class="mobile-menu-contact">
          <div class="mobile-phone">(844) 448-0110</div>
          <div class="mobile-hours">(9am to 6pm CST, Mon-Sat)</div>
        </div>
        <button class="mobile-listing-button" @click="closeMobileMenu">
          Start Free Listing
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onBeforeUnmount } from 'vue'
import GroupIcon from '../icons/Group.svg'
import Path3450Icon from '../icons/Path 3450.svg'
import Path3451Icon from '../icons/Path 3451.svg'
import Path3557Icon from '../icons/Path 3557.svg'
import Path3452Icon from '../icons/Path 3452.svg'

const isMobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  if (isMobileMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
  document.body.style.overflow = ''
}

onBeforeUnmount(() => {
  document.body.style.overflow = ''
})
</script>

<style>
.header-wrapper {
  width: 100%;
  height: 74px;
  position: relative;
  background-color: #fff;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 16px;
  gap: 16px;
  z-index: 1000;
}

/* Mobile Menu Button */
.mobile-menu-button {
  display: flex;
  align-items: center;
  justify-content: center;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  height: 40px;
  width: 40px;
  flex-shrink: 0;
}

.menu-icon {
  width: 100%;
  height: 100%;
}

/* Logo */
.header-logo {
  height: 34.3px;
  width: auto;
  max-width: 117.6px;
  flex-shrink: 0;
  object-fit: contain;
}

/* Desktop Navigation */
.desktop-navigation {
  display: none;
  justify-content: center;
  align-items: center;
}

.group2 {
  display: flex;
  align-items: center;
  gap: 14px;
  font-size: 14px;
  color: #000;
}

.how-houzeo-works,
.reviews,
.pricing,
.sign-in {
  cursor: pointer;
  white-space: nowrap;
  transition: color 0.2s;
}

.how-houzeo-works:hover,
.reviews:hover,
.pricing:hover,
.sign-in:hover {
  color: #0B5AA5;
}

.group3,
.group4,
.group5,
.group6 {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  transition: color 0.2s;
}

.group3:hover,
.group4:hover,
.group5:hover,
.group6:hover {
  color: #0B5AA5;
}

.sell,
.buy,
.product,
.resources {
  white-space: nowrap;
}

.path-3450-icon,
.path-3451-icon,
.path-3557-icon,
.path-3452-icon {
  width: 11px;
  height: 5px;
  object-fit: contain;
}

/* Desktop Actions */
.desktop-actions {
  display: none;
  align-items: center;
  gap: 24px;
}

.am-to-6pm-cst-mon-sat {
  display: flex;
  flex-direction: column;
  gap: 2px;
  margin-left: 6px;
}

.div {
  font-size: 14px;
  color: #000;
  white-space: nowrap;
}

.am-to-6pm {
  font-size: 12px;
  color: #000;
  white-space: nowrap;
}

.group {
  display: flex;
  align-items: center;
  justify-content: center;
}

.start-free-listing {
  padding: 12px 24px;
  background: linear-gradient(90deg, #2876C1 0%, #0E5293 100%);
  color: #fff;
  font-size: 14px;
  font-weight: 500;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  white-space: nowrap;
  transition: opacity 0.2s;
  margin-left: 18px;
}

.start-free-listing:hover {
  opacity: 0.9;
}

/* Mobile Action Button */
.mobile-action-button {
  display: flex;
  align-items: center;
  justify-content: center;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  height: 27.4px;
  width: 27.4px;
  flex-shrink: 0;
}

.action-icon {
  width: 100%;
  height: 100%;
}

/* Mobile Menu Overlay */
.mobile-menu-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 999;
  animation: fadeIn 0.3s ease;
}

/* Mobile Menu */
.mobile-menu {
  position: fixed;
  top: 74px;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #fff;
  z-index: 1000;
  transform: translateX(-100%);
  transition: transform 0.3s ease;
  overflow-y: auto;
}

.mobile-menu-open {
  transform: translateX(0);
}

.mobile-menu-content {
  padding: 24px 16px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.mobile-menu-item {
  padding: 12px 0;
  font-size: 16px;
  color: #000;
  cursor: pointer;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  transition: color 0.2s;
}

.mobile-menu-item:hover {
  color: #0B5AA5;
}

.dropdown-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.dropdown-icon {
  width: 11px;
  height: 5px;
  object-fit: contain;
}

.mobile-menu-contact {
  padding: 16px 0;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  margin-top: 8px;
}

.mobile-phone {
  font-size: 16px;
  font-weight: 500;
  color: #000;
  margin-bottom: 4px;
}

.mobile-hours {
  font-size: 14px;
  color: rgba(0, 0, 0, 0.6);
}

.mobile-listing-button {
  width: 100%;
  padding: 14px 24px;
  background: linear-gradient(90deg, #2876C1 0%, #0E5293 100%);
  color: #fff;
  font-size: 16px;
  font-weight: 500;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  margin-top: 8px;
  transition: opacity 0.2s;
}

.mobile-listing-button:hover {
  opacity: 0.9;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Tablet and Desktop Styles */
@media (min-width: 768px) {
  .header-wrapper {
    padding: 0 24px;
    gap: 24px;
  }

  .header-logo {
    max-width: 124px;
    height: 34.3px;
  }
}

@media (min-width: 1024px) {
  .header-wrapper {
    padding: 0 24px;
    gap: 40px;
    height: 74px;
  }

  .mobile-menu-button {
    display: none;
  }

  .mobile-action-button {
    display: none;
  }

  .desktop-navigation {
    display: flex;
    justify-content: center;
  }

  .group2 {
    display: flex;
    align-items: center;
    gap: 24px;
    font-size: 14px;
  }

  .desktop-actions {
    display: flex;
  }

  .mobile-menu {
    display: none;
  }

  .mobile-menu-overlay {
    display: none;
  }

  .header-logo {
    max-width: 117.6px;
    height: 34.3px;
  }
}

/* iPhone 14 Pro Max (428px) and smaller */
@media (max-width: 428px) {
  .header-wrapper {
    padding: 0 12px;
    gap: 10px;
    height: 56px;
  }

  .header-logo {
    max-width: 90px;
    height: auto;
    max-height: 26px;
  }

  .mobile-menu-button {
    padding: 5px;
    height: 22px;
    width: 22px;
  }

  .mobile-action-button {
    height: 22px;
    width: 22px;
  }
}

/* Responsive adjustments for smaller screens */
@media (max-width: 480px) {
  .header-wrapper {
    padding: 0 16px;
    gap: 12px;
    height: 60px;
  }

  .header-logo {
    max-width: 100px;
    height: auto;
    max-height: 28px;
  }

  .mobile-menu-button {
    padding: 6px;
    height: 34px;
    width: 34px;
  }

  .mobile-action-button {
    height: 24px;
    width: 24px;
  }
}
</style>
