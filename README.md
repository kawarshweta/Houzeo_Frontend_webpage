# Real Estate Search Page

A responsive real estate search page built with Vue.js 3, featuring an interactive map, property listings with image sliders, and smooth animations.

![Vue.js](https://img.shields.io/badge/Vue.js-3.x-4FC08D?style=flat-square&logo=vue.js)
![Vite](https://img.shields.io/badge/Vite-7.x-646CFF?style=flat-square&logo=vite)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3)

## Features

### Core Features
- 🏠 **Property Listings** - Display property cards with comprehensive details
- 🗺️ **Interactive Map** - Leaflet-powered map with property markers
- 🔍 **Filter Bar** - Status, price, bedrooms, and property type filters
- 📱 **Responsive Design** - Optimized for desktop and mobile (iPhone 14 Pro Max)
- 🎨 **Modern UI/UX** - Clean, intuitive interface with smooth transitions

### Animations & Effects
- ❤️ **Pulse Effect** - Heart icon animates on hover
- 🖼️ **Image Slider** - Navigate property images with arrows and dots
- 📦 **Card Hover** - Box shadow effect on property cards
- 🎯 **Input Transitions** - Smooth border color changes on filter inputs

### Performance Optimizations
- ⚡ **Lazy Loading** - Images load as they enter the viewport
- 🔄 **Intersection Observer** - Efficient visibility detection
- 🚀 **Vite Build** - Fast development and optimized production builds

## Project Structure

```
Frontend_Assignment/
├── public/
│   └── vite.svg
├── src/
│   ├── components/
│   │   ├── Header.vue          # Navigation header with centered logo
│   │   ├── FilterBar.vue       # Search and filter controls
│   │   ├── MapSection.vue      # Leaflet map integration
│   │   ├── PropertyList.vue    # Property cards grid
│   │   ├── PropertyCard.vue    # Individual property card
│   │   ├── ImageSlider.vue     # Image carousel with lazy loading
│   │   └── SortDropdown.vue    # Sort by dropdown menu
│   ├── App.vue                 # Main application component
│   ├── main.js                 # Vue app initialization
│   └── style.css               # Global CSS styles
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

## Prerequisites

- Node.js (v18.0.0 or higher recommended)
- npm or yarn

## Setup Instructions

### 1. Clone or Extract the Project

```bash
# If using git
git clone <repository-url>
cd Frontend_Assignment

# Or extract the ZIP file and navigate to the folder
cd Frontend_Assignment
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Run Development Server

```bash
npm run dev
```

The application will start at `http://localhost:5173`

### 4. Build for Production

```bash
npm run build
```

The production files will be generated in the `dist` folder.

### 5. Preview Production Build

```bash
npm run preview
```

## Responsive Breakpoints

| Device | Width | Layout |
|--------|-------|--------|
| Mobile (iPhone 14 Pro Max) | < 1024px | Stacked layout, collapsible map |
| Desktop | ≥ 1024px | Side-by-side (map left, listings right) |

## Component Details

### Header Component
- Centered logo design
- Mobile hamburger menu
- Saved properties and user account buttons

### Filter Bar
- Search input with icon
- Status dropdown (For Sale, Sold, For Rent)
- Price range filter
- Bedrooms filter
- Property type filter
- Save Search button
- **Hover Effect**: Border color transitions smoothly on all inputs

### Map Section
- Interactive Leaflet map centered on US
- Custom markers showing property prices
- Click markers for property popups
- Responsive sizing

### Property Cards
- **Image Slider**: 
  - Navigate with arrows (visible on hover)
  - Dot indicators for image count
  - Lazy loading for performance
- Property details: beds, baths, sqft
- Address display
- Days on market badge
- **Heart Icon**: Pulse animation on hover
- **Card Hover**: Elevated box shadow effect

### Sort Dropdown
- Multiple sorting options
- Smooth dropdown animation
- Active state highlighting

## Technologies Used

- **Vue.js 3** - Progressive JavaScript framework
- **Vite** - Next generation frontend tooling
- **HTML5 & CSS3** - Pure HTML and CSS for styling (no CSS frameworks)
- **Leaflet** - Interactive maps library
- **@vueuse/core** - Vue composition utilities

## Browser Compatibility

Tested and compatible with:
- Google Chrome (latest)
- Mozilla Firefox (latest)
- Safari (latest)
- Microsoft Edge (latest)

## Performance Features

1. **Lazy Loading Images**: Images load only when visible in viewport
2. **CSS Animations**: Hardware-accelerated transitions
3. **Optimized Bundle**: Vite tree-shaking and code splitting
4. **Efficient State Management**: Vue 3 Composition API reactivity

## Customization

### Adding Properties
Edit the `properties` array in `src/App.vue`:

```javascript
const properties = ref([
  {
    id: 7,
    type: 'House For Sale',
    price: 550000,
    bedrooms: 4,
    bathrooms: 3,
    sqft: 2800,
    address: '123 New Street, City, TX 00000',
    daysOnMarket: 5,
    isFavorite: false,
    images: ['url1', 'url2', 'url3'],
    coordinates: [latitude, longitude],
  },
  // ... more properties
])
```

### Changing Colors
Modify the color palette in `src/style.css` using CSS variables:

```css
:root {
  --color-primary: #1a73e8;    /* Main brand color */
  --color-secondary: #34a853;  /* Secondary color */
  --color-accent: #ea4335;     /* Accent color */
}
```

## License

This project is created for assessment purposes.

## Author

Developed as part of a Frontend Developer assignment.
