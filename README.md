# 🌍 Wanderwise - Smart Travel Planner

<div align="center">

![Wanderwise Logo](https://img.shields.io/badge/Wanderwise-AI%20Travel%20Planner-2C7BE5?style=for-the-badge&logo=airplane)

**Intelligent travel planning powered by AI** ✈️

[![Vue.js](https://img.shields.io/badge/Vue.js-3.4.38-4FC08D?style=flat-square&logo=vue.js)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.5.3-3178C6?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![Naive UI](https://img.shields.io/badge/Naive%20UI-2.42.0-18A058?style=flat-square)](https://www.naiveui.com/)
[![Vite](https://img.shields.io/badge/Vite-5.4.2-646CFF?style=flat-square&logo=vite)](https://vitejs.dev/)

[Live Demo](https://wanderwise-demo.netlify.app) • [Documentation](https://wanderwise-docs.netlify.app) • [Issues](https://github.com/wanderwise/issues)

</div>

---

## ✨ Features

### 🎯 **Smart Trip Planning**
- **AI-Powered Recommendations** - Get personalized suggestions for flights, hotels, and activities
- **Intelligent Itinerary Builder** - Create day-by-day schedules based on your interests
- **Weather Integration** - Real-time weather forecasts for your destination
- **Budget Optimization** - Find the best deals within your budget range

### 🎨 **Modern Design**
- **Beautiful UI/UX** - Clean, modern interface with smooth animations
- **Responsive Design** - Works perfectly on desktop, tablet, and mobile
- **Dark/Light Themes** - Choose your preferred visual style
- **Accessibility First** - WCAG compliant for inclusive design

### 🚀 **User Experience**
- **Step-by-Step Flow** - Guided planning process with progress tracking
- **Real-time Updates** - Instant feedback and dynamic content
- **Save & Resume** - Continue planning where you left off
- **Export Options** - Download your itinerary as PDF or share via email

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **Vue.js** | 3.4.38 | Progressive JavaScript framework |
| **TypeScript** | 5.5.3 | Type-safe JavaScript development |
| **Naive UI** | 2.42.0 | Vue 3 component library |
| **Vite** | 5.4.2 | Fast build tool and dev server |
| **Inter Font** | Latest | Modern, readable typography |

---

## 🎨 Design System

### Color Palette
```css
--primary: #2C7BE5      /* Main brand color */
--accent-1: #00C9A7     /* Success states */
--accent-2: #FFC107     /* Warnings & highlights */
--background: #F8F9FA   /* Page background */
--card-bg: #FFFFFF      /* Card backgrounds */
--text: #212529         /* Primary text */
```

### Typography
- **Font Family**: Inter (Google Fonts)
- **Weights**: 400 (body), 600 (headings), 700 (emphasis)
- **Line Height**: 1.6 for optimal readability

### Components
- **Cards**: Rounded corners with subtle shadows
- **Buttons**: Gradient backgrounds with hover effects
- **Forms**: Clean inputs with focus states
- **Navigation**: Sticky header with smooth transitions

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/wanderwise.git
   cd wanderwise
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   ```
   http://localhost:5173
   ```

### Build for Production

```bash
npm run build
npm run preview
```

---

## 📱 User Flow

### 1. **Trip Setup** 🎯
- Enter destination and travel dates
- Select trip type (Solo, Family, Business, etc.)
- Set budget preferences

### 2. **Flight Selection** ✈️
- AI-recommended flights based on preferences
- Filter by price, duration, and stops
- Compare features and ratings

### 3. **Hotel Booking** 🏨
- Curated accommodation options
- Location-based recommendations
- Amenity filtering and reviews

### 4. **Weather Check** 🌤️
- 7-day weather forecast
- Packing suggestions
- Activity recommendations

### 5. **Itinerary Builder** 📅
- AI-generated day-by-day schedule
- Customizable activities and timing
- Local restaurant and attraction suggestions

### 6. **Trip Summary** 📋
- Complete trip overview
- Export and sharing options
- Emergency contact information

---

## 🎯 Key Features

### AI-Powered Recommendations
- **Smart Matching**: Algorithms that understand your preferences
- **Local Insights**: Recommendations from travel experts and locals
- **Real-time Updates**: Dynamic pricing and availability

### Interactive Planning
- **Drag & Drop**: Reorder activities and modify schedules
- **Real-time Collaboration**: Share plans with travel companions
- **Offline Support**: Access your itinerary without internet

### Safety & Support
- **Emergency Contacts**: Local emergency numbers and embassy info
- **Travel Alerts**: Real-time notifications about your destination
- **24/7 Support**: Round-the-clock customer assistance

---

## 🏗️ Project Structure

```
wanderwise/
├── src/
│   ├── components/          # Vue components
│   │   ├── Header.vue       # Navigation header
│   │   ├── HeroSearch.vue   # Main search interface
│   │   ├── FlightSelection.vue
│   │   ├── AccommodationSelection.vue
│   │   ├── WeatherInfo.vue
│   │   ├── ItineraryBuilder.vue
│   │   ├── TripSummary.vue
│   │   └── Footer.vue
│   ├── assets/              # Static assets
│   ├── style.css            # Global styles
│   ├── main.ts              # App entry point
│   └── App.vue              # Root component
├── public/                  # Public assets
├── package.json             # Dependencies
└── README.md               # This file
```

---

## 🎨 Customization

### Theme Customization
```css
/* Customize colors in src/style.css */
:root {
  --primary: #your-brand-color;
  --accent-1: #your-accent-color;
  /* ... other variables */
}
```

### Component Styling
```vue
<!-- Use CSS custom properties for consistent theming -->
<style scoped>
.my-component {
  background: var(--card-bg);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
}
</style>
```

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

### Code Style
- Follow Vue.js style guide
- Use TypeScript for type safety
- Write meaningful commit messages
- Add tests for new features

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Vue.js Team** - For the amazing framework
- **Naive UI** - For the beautiful component library
- **Inter Font** - For the modern typography
- **Travel Community** - For inspiration and feedback

---

## 📞 Support

- **Email**: support@wanderwise.com
- **Discord**: [Join our community](https://discord.gg/wanderwise)
- **Documentation**: [docs.wanderwise.com](https://docs.wanderwise.com)
- **Issues**: [GitHub Issues](https://github.com/wanderwise/issues)

---

<div align="center">

**Made with ❤️ by the Wanderwise Team**

[![GitHub stars](https://img.shields.io/github/stars/wanderwise/wanderwise?style=social)](https://github.com/wanderwise/wanderwise)
[![GitHub forks](https://img.shields.io/github/forks/wanderwise/wanderwise?style=social)](https://github.com/wanderwise/wanderwise)
[![GitHub issues](https://img.shields.io/github/issues/wanderwise/wanderwise)](https://github.com/wanderwise/wanderwise/issues)

</div>
