<script setup lang="ts">
import { ref } from 'vue'
import { 
  SparklesOutline, 
  LocationOutline, 
  AirplaneOutline, 
  BedOutline, 
  SunnyOutline, 
  MapOutline, 
  CheckmarkCircleOutline,
  HeartOutline,
  ShieldCheckmarkOutline,
  ShareSocialOutline,
  ArrowForwardOutline,
  ChatbubbleOutline,
  CloseOutline,
  CalendarOutline,
  WalletOutline,
  PeopleOutline
} from '@vicons/ionicons5'

const emit = defineEmits<{
  startPlanning: []
}>()

// Search form data
const searchForm = ref({
  destination: '',
  startDate: '',
  endDate: '',
  tripType: '',
  budget: ''
})

const tripTypes = [
  { value: 'solo', label: 'Solo', icon: '👤' },
  { value: 'family', label: 'Family', icon: '👨‍👩‍👧‍👦' },
  { value: 'work', label: 'Work', icon: '💼' },
  { value: 'honeymoon', label: 'Honeymoon', icon: '💕' }
]

const budgetRanges = [
  { value: 'budget', label: 'Budget', range: '$500-1000' },
  { value: 'moderate', label: 'Moderate', range: '$1000-2500' },
  { value: 'luxury', label: 'Luxury', range: '$2500+' }
]

// Trip resume data
const activeTrips = [
  {
    id: 1,
    destination: '🌴 Bali Family Trip',
    progress: 80,
    status: '80% Complete',
    lastActivity: 'Added hotel preferences'
  },
  {
    id: 2,
    destination: '🇯🇵 Japan Adventure',
    progress: 60,
    status: 'Flights Booked, Itinerary In Progress',
    lastActivity: 'Booked flights for March 15'
  }
]

// Trending destinations
const trendingDestinations = [
  { 
    name: 'Santorini', 
    image: 'https://images.unsplash.com/photo-1570077188670-e3a8d69ac5ff?w=400&h=300&fit=crop', 
    country: 'Greece',
    theme: 'Romantic Getaway',
    weather: '☀️ 28°C',
    priceRange: '$1000-1500',
    tags: ['🏝️ Beach', '💕 Romantic']
  },
  { 
    name: 'Banff', 
    image: 'https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=400&h=300&fit=crop', 
    country: 'Canada',
    theme: 'Nature + Adventure',
    weather: '❄️ 5°C',
    priceRange: '$600-900',
    tags: ['🏔️ Adventure', '🍁 Nature']
  },
  { 
    name: 'Bali', 
    image: 'https://images.unsplash.com/photo-1537953773345-d172ccf13cf1?w=400&h=300&fit=crop', 
    country: 'Indonesia',
    theme: 'Beach & Culture',
    weather: '🌤️ 30°C',
    priceRange: '$500-800',
    tags: ['🏝️ Beach', '🏛️ Culture']
  },
  { 
    name: 'Tokyo', 
    image: 'https://images.unsplash.com/photo-1540959733332-eab4deabeeaf?w=400&h=300&fit=crop', 
    country: 'Japan',
    theme: 'Food & Shopping',
    weather: '🌤️ 22°C',
    priceRange: '$800-1200',
    tags: ['🍜 Food', '🛍️ Shopping']
  }
]

// Inspiration categories
const inspirationCategories = [
  {
    title: '🍲 Best Food Cities for Fall',
    description: 'Discover culinary adventures in autumn',
    image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=300&h=200&fit=crop'
  },
  {
    title: '⛰️ Nature Escapes Within $800',
    description: 'Budget-friendly outdoor adventures',
    image: 'https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=300&h=200&fit=crop'
  },
  {
    title: '👩‍👩‍👧‍👦 Family-Friendly European Spots',
    description: 'Perfect destinations for the whole family',
    image: 'https://images.unsplash.com/photo-1502602898535-0e2b9b2b7b1a?w=300&h=200&fit=crop'
  }
]

const testimonials = [
  {
    quote: "We planned our 10-day Japan trip in 5 minutes. Everything was on point.",
    author: "🇨🇦 Alex Chen",
    trip: "Japan Adventure",
    avatar: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=60&h=60&fit=crop&crop=face"
  },
  {
    quote: "Wanderwise made our honeymoon completely stress-free.",
    author: "🇫🇷 Sarah & Mike",
    trip: "Paris Honeymoon",
    avatar: "https://images.unsplash.com/photo-1494790108755-2616b612b786?w=60&h=60&fit=crop&crop=face"
  },
  {
    quote: "The AI suggestions were spot-on. Found hidden gems we never would have discovered.",
    author: "🇪🇸 Maria Rodriguez",
    trip: "Bali Family Trip",
    avatar: "https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=60&h=60&fit=crop&crop=face"
  }
]

const features = [
  {
    icon: SparklesOutline,
    title: "AI-Powered Planning",
    description: "Personalized trip flows that adapt to your preferences and travel style"
  },
  {
    icon: HeartOutline,
    title: "Smart Suggestions",
    description: "Packing lists, restaurant recommendations, and local insights tailored just for you"
  },
  {
    icon: ShareSocialOutline,
    title: "Save & Share Trips",
    description: "Sync your itineraries across devices and share with travel companions"
  },
  {
    icon: ShieldCheckmarkOutline,
    title: "Privacy First",
    description: "Your data stays yours. We never sell or share your personal information"
  }
]

const steps = [
  { icon: LocationOutline, label: "Intent", description: "Destination, dates, type, budget" },
  { icon: AirplaneOutline, label: "Flights", description: "Best options via AI (price + comfort)" },
  { icon: BedOutline, label: "Hotels", description: "Matches your vibe (luxury, budget, scenic)" },
  { icon: SunnyOutline, label: "Weather", description: "Forecast + packing tips" },
  { icon: MapOutline, label: "Itinerary", description: "Auto-built based on pace & preferences" },
  { icon: CheckmarkCircleOutline, label: "Final Review", description: "Share, export, or revisit your plan" }
]

// Floating assistant
const showAssistant = ref(true)
const assistantMessage = ref("Looks like you're planning a trip to Paris. Want help finding activities for Day 3?")

const handleStartPlanning = () => {
  emit('startPlanning')
}

const closeAssistant = () => {
  showAssistant.value = false
}

const handleSearch = () => {
  // Handle search form submission
  console.log('Search submitted:', searchForm.value)
  handleStartPlanning()
}
</script>

<template>
  <div class="homepage">
    <!-- Hero Section with Search -->
    <section class="hero-section">
      <img 
        src="https://images.unsplash.com/photo-1488646953014-85cb44e25828?w=1920&h=1080&fit=crop&auto=format&q=80" 
        alt="Travel background"
        class="hero-bg-image"
        @load="console.log('Hero image loaded successfully')"
        @error="console.log('Hero image failed to load:', $event.target.src)"
      />
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="hero-badge">
          <n-icon size="24" color="#6366F1">
            <SparklesOutline />
          </n-icon>
          <span>🧠 AI‑Powered Travel Companion</span>
        </div>
        
        <div class="hero-text-container">
          <h1 class="hero-title">
            Where to?
          </h1>
          
          <p class="hero-subtitle">
            Plan your perfect trip with AI-powered suggestions
          </p>
        </div>
        
        <!-- Hero Search Bar -->
        <div class="hero-search-container">
          <div class="search-form">
            <div class="search-row">
              <div class="search-field">
                <n-icon size="20" color="#6366F1">
                  <LocationOutline />
                </n-icon>
                <input 
                  v-model="searchForm.destination"
                  type="text" 
                  placeholder="Where do you want to go?"
                  class="search-input"
                />
              </div>
              
              <div class="search-field">
                <n-icon size="20" color="#6366F1">
                  <CalendarOutline />
                </n-icon>
                <input 
                  v-model="searchForm.startDate"
                  type="date" 
                  class="search-input"
                />
              </div>
              
              <div class="search-field">
                <n-icon size="20" color="#6366F1">
                  <CalendarOutline />
                </n-icon>
                <input 
                  v-model="searchForm.endDate"
                  type="date" 
                  class="search-input"
                />
              </div>
            </div>
            
            <div class="search-row">
              <div class="search-field">
                <n-icon size="20" color="#6366F1">
                  <PeopleOutline />
                </n-icon>
                <select v-model="searchForm.tripType" class="search-input">
                  <option value="">Trip Type</option>
                  <option v-for="type in tripTypes" :key="type.value" :value="type.value">
                    {{ type.icon }} {{ type.label }}
                  </option>
                </select>
              </div>
              
              <div class="search-field">
                <n-icon size="20" color="#6366F1">
                  <WalletOutline />
                </n-icon>
                <select v-model="searchForm.budget" class="search-input">
                  <option value="">Budget</option>
                  <option v-for="budget in budgetRanges" :key="budget.value" :value="budget.value">
                    {{ budget.label }} ({{ budget.range }})
                  </option>
                </select>
              </div>
              
              <div class="search-actions">
                <n-button 
                  type="primary" 
                  size="large" 
                  class="search-cta"
                  @click="handleSearch"
                >
                  <template #icon>
                    <n-icon><SparklesOutline /></n-icon>
                  </template>
                  📍 Plan My Trip
                </n-button>
                
                <n-button 
                  size="large" 
                  class="explore-button"
                  ghost
                >
                  💡 Explore Ideas
                </n-button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Scroll indicator -->
        <div class="scroll-indicator">
          <span>↓ Scroll to begin</span>
        </div>
      </div>
    </section>

    <!-- Resume Where You Left Off -->
    <section class="resume-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Resume Where You Left Off</h2>
          <p class="section-subtitle">Continue planning your adventures</p>
        </div>
        
        <div class="trip-resume-grid">
          <div 
            v-for="trip in activeTrips" 
            :key="trip.id"
            class="trip-resume-card"
          >
            <div class="trip-info">
              <h3 class="trip-destination">{{ trip.destination }}</h3>
              <p class="trip-status">{{ trip.status }}</p>
              <p class="trip-activity">{{ trip.lastActivity }}</p>
            </div>
            <div class="trip-progress">
              <div class="progress-bar">
                <div class="progress-fill" :style="{ width: trip.progress + '%' }"></div>
              </div>
              <span class="progress-text">{{ trip.progress }}%</span>
            </div>
            <n-button size="small" type="primary" class="resume-button">
              Resume
            </n-button>
          </div>
          
          <div class="view-all-trips">
            <n-button size="large" ghost class="view-all-button">
              ➕ View All Trips
              <template #icon>
                <n-icon><ArrowForwardOutline /></n-icon>
              </template>
            </n-button>
          </div>
        </div>
      </div>
    </section>

    <!-- Trending Destinations -->
    <section class="trending-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">💡 Trending Destinations</h2>
          <p class="section-subtitle">Get inspired by what's popular right now</p>
        </div>
        
        <div class="trending-grid">
          <div 
            v-for="destination in trendingDestinations" 
            :key="destination.name"
            class="trending-card"
          >
            <div class="trending-image">
              <img 
                :src="destination.image" 
                :alt="destination.name"
                @error="$event.target.src='https://picsum.photos/400/300?random=100'"
                loading="lazy"
              />
              <div class="trending-tags">
                <span 
                  v-for="tag in destination.tags" 
                  :key="tag"
                  class="trending-tag"
                >
                  {{ tag }}
                </span>
              </div>
              <div class="trending-overlay">
                <div class="trending-info">
                  <h3 class="trending-name">{{ destination.name }}</h3>
                  <p class="trending-country">{{ destination.country }}</p>
                  <p class="trending-theme">{{ destination.theme }}</p>
                  <div class="trending-details">
                    <span class="weather-info">{{ destination.weather }}</span>
                    <span class="price-info">{{ destination.priceRange }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Smart Steps Section -->
    <section class="smart-steps">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">🧳 Plan Your Trip in 6 Smart Steps</h2>
          <p class="section-subtitle">Wanderwise does the heavy lifting. You just enjoy the journey.</p>
        </div>
        
        <div class="steps-grid">
          <div 
            v-for="(step, index) in steps" 
            :key="index"
            class="step-card"
          >
            <div class="step-icon">
              <n-icon size="32" color="#6366F1">
                <component :is="step.icon" />
              </n-icon>
            </div>
            <h3 class="step-label">{{ step.label }}</h3>
            <p class="step-description">{{ step.description }}</p>
            <div class="step-number">{{ index + 1 }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Why Wanderwise Section -->
    <section class="why-wanderwise">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">❤️ Why People Love Wanderwise</h2>
          <p class="section-subtitle">Built for modern travelers who want more than just a booking site.</p>
        </div>
        
        <div class="features-grid">
          <div 
            v-for="feature in features" 
            :key="feature.title"
            class="feature-card"
          >
            <div class="feature-icon">
              <n-icon size="40" color="#6366F1">
                <component :is="feature.icon" />
              </n-icon>
            </div>
            <h3 class="feature-title">{{ feature.title }}</h3>
            <p class="feature-description">{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <section class="testimonials">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Traveler Voices</h2>
          <p class="section-subtitle">See what our users are saying about their Wanderwise experiences.</p>
        </div>
        
        <div class="testimonials-grid">
          <div 
            v-for="(testimonial, index) in testimonials" 
            :key="testimonial.author"
            class="testimonial-card"
            :class="`testimonial-${index % 2 === 0 ? 'light' : 'dark'}`"
          >
            <div class="testimonial-content">
              <p class="testimonial-quote">"{{ testimonial.quote }}"</p>
            </div>
            <div class="testimonial-author">
              <img 
                :src="testimonial.avatar" 
                :alt="testimonial.author" 
                class="author-avatar"
                @error="$event.target.style.display='none'"
              />
              <div class="author-info">
                <h4 class="author-name">{{ testimonial.author }}</h4>
                <p class="author-trip">{{ testimonial.trip }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Inspiration Board -->
    <section class="inspiration-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">✈️ Just Browsing? Explore Ideas</h2>
          <p class="section-subtitle">Discover inspiration for your next adventure</p>
        </div>
        
        <div class="inspiration-grid">
          <div 
            v-for="category in inspirationCategories" 
            :key="category.title"
            class="inspiration-card"
          >
            <div class="inspiration-image">
              <img 
                :src="category.image" 
                :alt="category.title"
                @error="$event.target.src='https://picsum.photos/300/200?random=200'"
                loading="lazy"
              />
              <div class="inspiration-overlay">
                <h3 class="inspiration-title">{{ category.title }}</h3>
                <p class="inspiration-description">{{ category.description }}</p>
              </div>
            </div>
          </div>
        </div>
        
        <div class="inspiration-filters">
          <span class="filter-tag">Beach</span>
          <span class="filter-tag">Culture</span>
          <span class="filter-tag">Romantic</span>
          <span class="filter-tag">Budget</span>
          <span class="filter-tag">Solo</span>
        </div>
      </div>
    </section>

    <!-- Final CTA Section -->
    <section class="final-cta">
      <div class="container">
        <div class="cta-content">
          <h2 class="cta-title">Ready to plan your perfect trip?</h2>
          <p class="cta-subtitle">Join thousands of travelers who trust Wanderwise to create unforgettable experiences.</p>
          
          <div class="cta-actions">
            <n-button 
              type="primary" 
              size="large" 
              class="cta-button"
              @click="handleStartPlanning"
            >
              <template #icon>
                <n-icon><SparklesOutline /></n-icon>
              </template>
              Launch Wanderwise Assistant
            </n-button>
            
            <n-button 
              size="large" 
              class="browse-button"
              ghost
            >
              Browse Destinations
              <template #icon>
                <n-icon><ArrowForwardOutline /></n-icon>
              </template>
            </n-button>
          </div>
        </div>
      </div>
    </section>

    <!-- Floating Assistant Bubble -->
    <div v-if="showAssistant" class="floating-assistant">
      <div class="assistant-content">
        <div class="assistant-header">
          <span class="assistant-title">🤖 Powered by Wanderwise Assistant</span>
          <button class="close-assistant" @click="closeAssistant">
            <n-icon size="16">
              <CloseOutline />
            </n-icon>
          </button>
        </div>
        <p class="assistant-message">{{ assistantMessage }}</p>
        <n-button size="small" type="primary" class="assistant-cta">
          <template #icon>
            <n-icon><ChatbubbleOutline /></n-icon>
          </template>
          Ask Assistant
        </n-button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.homepage {
  min-height: 100vh;
}

/* Hero Section */
.hero-section {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: white;
  overflow: hidden;
}

.hero-bg-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  z-index: 0;
  opacity: 1;
  visibility: visible;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(0, 0, 0, 0.4) 0%, rgba(0, 201, 167, 0.6) 100%);
  z-index: 1;
}

.hero-content {
  max-width: 800px;
  padding: var(--spacing-2xl);
  z-index: 2;
  position: relative;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border-radius: var(--radius-xl);
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-sm);
  background: rgba(0, 0, 0, 0.6);
  color: white;
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--radius-xl);
  font-weight: 600;
  font-size: 0.9rem;
  margin-bottom: var(--spacing-xl);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.hero-text-container {
  margin-bottom: var(--spacing-2xl);
}

.hero-title {
  font-size: 4rem;
  font-weight: 900;
  margin: 0 0 var(--spacing-lg) 0;
  line-height: 1.1;
  letter-spacing: -2px;
  color: white;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.title-highlight {
  background: linear-gradient(135deg, #F59E0B 0%, #EC4899 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: none;
}

.hero-subtitle {
  font-size: 1.5rem;
  margin: 0 0 var(--spacing-2xl) 0;
  line-height: 1.6;
  color: white;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
}

.hero-search-container {
  margin-top: var(--spacing-2xl);
  padding: var(--spacing-lg);
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: var(--radius-lg);
  border: 1px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.search-form {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.search-row {
  display: flex;
  gap: var(--spacing-md);
  align-items: center;
  flex-wrap: wrap;
}

.search-field {
  display: flex;
  align-items: center;
  background: rgba(255, 255, 255, 0.2);
  border-radius: var(--radius-md);
  padding: var(--spacing-sm) var(--spacing-md);
  border: 1px solid rgba(255, 255, 255, 0.3);
  flex: 1;
  min-width: 150px;
}

.search-input {
  background: none;
  border: none;
  color: white;
  font-size: 1rem;
  width: 100%;
  outline: none;
}

.search-input::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

.search-actions {
  display: flex;
  gap: var(--spacing-md);
  justify-content: center;
  flex-wrap: wrap;
}

.search-cta {
  height: 56px;
  font-weight: 700;
  font-size: 1.1rem;
  background: var(--gradient-primary) !important;
  border: none !important;
  border-radius: var(--radius-lg);
  transition: all 0.3s ease;
  flex: 1;
  min-width: 200px;
}

.search-cta:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 12px 35px rgba(99, 102, 241, 0.4);
}

.explore-button {
  height: 56px;
  font-weight: 600;
  font-size: 1.1rem;
  border-radius: var(--radius-lg);
  border: 2px solid rgba(255, 255, 255, 0.3);
  color: white;
  transition: all 0.3s ease;
  flex: 1;
  min-width: 200px;
}

.explore-button:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-3px) scale(1.05);
}

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  color: white;
  font-size: 0.9rem;
  font-weight: 600;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
  z-index: 3;
}



/* Container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--spacing-lg);
}

/* Section Headers */
.section-header {
  text-align: center;
  margin-bottom: var(--spacing-3xl);
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  color: var(--text);
  margin: 0 0 var(--spacing-md) 0;
  line-height: 1.2;
}

.section-subtitle {
  font-size: 1.3rem;
  color: var(--text-light);
  margin: 0;
  line-height: 1.6;
  max-width: 600px;
  margin: 0 auto;
}

/* Resume Where You Left Off */
.resume-section {
  padding: var(--spacing-3xl) 0;
  background: var(--background);
}

.trip-resume-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: var(--spacing-lg);
}

.trip-resume-card {
  background: white;
  padding: var(--spacing-2xl);
  border-radius: var(--radius-xl);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  border: 1px solid var(--border-light);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.trip-resume-card:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.trip-info {
  margin-bottom: var(--spacing-md);
}

.trip-destination {
  font-size: 1.3rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-xs) 0;
}

.trip-status {
  font-size: 0.9rem;
  color: var(--text-light);
  margin: 0 0 var(--spacing-xs) 0;
}

.trip-activity {
  font-size: 0.8rem;
  color: var(--text-light);
  margin: 0;
}

.trip-progress {
  width: 100%;
  margin-bottom: var(--spacing-md);
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
}

.progress-bar {
  flex-grow: 1;
  height: 8px;
  background: var(--border-light);
  border-radius: 4px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: var(--gradient-primary);
  border-radius: 4px;
  transition: width 0.3s ease-in-out;
}

.progress-text {
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--text);
}

.resume-button {
  width: 100%;
  font-weight: 700;
  font-size: 1rem;
  background: var(--gradient-primary) !important;
  border: none !important;
  border-radius: var(--radius-md);
  transition: all 0.3s ease;
}

.resume-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(99, 102, 241, 0.3);
}

.view-all-trips {
  width: 100%;
  text-align: center;
}

.view-all-button {
  height: 56px;
  font-weight: 600;
  font-size: 1.1rem;
  border-radius: var(--radius-lg);
  border: 2px solid rgba(255, 255, 255, 0.3);
  color: white;
  transition: all 0.3s ease;
}

.view-all-button:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-3px);
}

/* Trending Destinations */
.trending-section {
  padding: var(--spacing-3xl) 0;
  background: white;
}

.trending-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-lg);
}

.trending-card {
  border-radius: var(--radius-xl);
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  cursor: pointer;
}

.trending-card:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.trending-image {
  position: relative;
  height: 200px;
  overflow: hidden;
  background: transparent;
}

.trending-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.trending-card:hover .trending-image img {
  transform: scale(1.1);
}

.trending-tags {
  position: absolute;
  top: var(--spacing-md);
  left: var(--spacing-md);
  background: rgba(0, 0, 0, 0.6);
  border-radius: var(--radius-md);
  padding: var(--spacing-xs) var(--spacing-sm);
  display: flex;
  gap: var(--spacing-xs);
  z-index: 2;
}

.trending-tag {
  font-size: 0.7rem;
  font-weight: 600;
  color: white;
  background: var(--gradient-primary);
  border-radius: var(--radius-sm);
  padding: var(--spacing-xs) var(--spacing-sm);
  white-space: nowrap;
}

.trending-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  color: white;
  padding: var(--spacing-lg);
  z-index: 2;
}

.trending-info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.trending-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0 0 var(--spacing-xs) 0;
}

.trending-country {
  margin: 0;
  opacity: 0.9;
}

.trending-theme {
  font-size: 0.9rem;
  color: var(--text-light);
  margin: 0;
}

.trending-details {
  display: flex;
  gap: var(--spacing-md);
  font-size: 0.9rem;
  color: var(--text-light);
  margin-top: var(--spacing-xs);
}

.weather-info {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
}

.price-info {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
}

/* Smart Steps Section */
.smart-steps {
  padding: var(--spacing-3xl) 0;
  background: var(--background);
}

.steps-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--spacing-xl);
}

.step-card {
  background: white;
  padding: var(--spacing-2xl);
  border-radius: var(--radius-xl);
  text-align: center;
  position: relative;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  border: 1px solid var(--border-light);
}

.step-card:hover {
  transform: translateY(-8px) scale(1.03);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.step-icon {
  width: 80px;
  height: 80px;
  background: var(--gradient-primary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto var(--spacing-lg) auto;
  color: white;
}

.step-label {
  font-size: 1.3rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-sm) 0;
}

.step-description {
  color: var(--text-light);
  margin: 0;
  line-height: 1.6;
}

.step-number {
  position: absolute;
  top: -15px;
  right: -15px;
  width: 40px;
  height: 40px;
  background: var(--gradient-primary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 700;
  font-size: 1.1rem;
}

/* Why Wanderwise Section */
.why-wanderwise {
  padding: var(--spacing-3xl) 0;
  background: white;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-xl);
}

.feature-card {
  padding: var(--spacing-2xl);
  border-radius: var(--radius-xl);
  text-align: center;
  transition: all 0.3s ease;
  border: 1px solid var(--border-light);
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-card);
}

.feature-icon {
  width: 80px;
  height: 80px;
  background: var(--gradient-primary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto var(--spacing-lg) auto;
  color: white;
}

.feature-title {
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-md) 0;
}

.feature-description {
  color: var(--text-light);
  margin: 0;
  line-height: 1.6;
}

/* Testimonials Section */
.testimonials {
  padding: var(--spacing-3xl) 0;
  background: var(--background);
}

.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: var(--spacing-xl);
}

.testimonial-card {
  background: white;
  padding: var(--spacing-2xl);
  border-radius: var(--radius-xl);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  border: 1px solid var(--border-light);
}

.testimonial-card.testimonial-light {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
}

.testimonial-card.testimonial-dark {
  background: linear-gradient(135deg, #1e293b 0%, #334155 100%);
  color: white;
}

.testimonial-card.testimonial-dark .testimonial-quote,
.testimonial-card.testimonial-dark .author-name {
  color: white;
}

.testimonial-card.testimonial-dark .author-trip {
  color: rgba(255, 255, 255, 0.7);
}

.testimonial-card:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.testimonial-quote {
  font-size: 1.1rem;
  line-height: 1.7;
  color: var(--text);
  margin: 0 0 var(--spacing-lg) 0;
  font-style: italic;
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
}

.author-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
}

.author-name {
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-xs) 0;
}

.author-trip {
  color: var(--text-light);
  margin: 0;
  font-size: 0.9rem;
}

/* Inspiration Board */
.inspiration-section {
  padding: var(--spacing-3xl) 0;
  background: var(--background);
}

.inspiration-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-lg);
}

.inspiration-card {
  border-radius: var(--radius-xl);
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  cursor: pointer;
}

.inspiration-card:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.inspiration-image {
  position: relative;
  height: 200px;
  overflow: hidden;
  background: transparent;
}

.inspiration-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.inspiration-card:hover .inspiration-image img {
  transform: scale(1.1);
}

.inspiration-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  color: white;
  padding: var(--spacing-lg);
  z-index: 2;
}

.inspiration-title {
  font-size: 1.3rem;
  font-weight: 700;
  margin: 0 0 var(--spacing-xs) 0;
}

.inspiration-description {
  font-size: 0.9rem;
  color: var(--text-light);
  margin: 0;
}

.inspiration-filters {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-sm);
  margin-top: var(--spacing-md);
  justify-content: center;
}

.filter-tag {
  background: var(--border-light);
  color: var(--text);
  padding: var(--spacing-xs) var(--spacing-md);
  border-radius: var(--radius-md);
  font-size: 0.8rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-tag:hover {
  background: var(--border-light);
  color: var(--text);
}

/* Final CTA Section */
.final-cta {
  padding: var(--spacing-3xl) 0;
  background: var(--gradient-primary);
  color: white;
  text-align: center;
}

.cta-content {
  max-width: 600px;
  margin: 0 auto;
}

.cta-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin: 0 0 var(--spacing-md) 0;
  line-height: 1.2;
}

.cta-subtitle {
  font-size: 1.2rem;
  margin: 0 0 var(--spacing-2xl) 0;
  line-height: 1.6;
  opacity: 0.9;
}

.cta-actions {
  display: flex;
  gap: var(--spacing-lg);
  justify-content: center;
  flex-wrap: wrap;
}

.browse-button {
  height: 56px;
  font-weight: 600;
  font-size: 1.1rem;
  border-radius: var(--radius-lg);
  border: 2px solid rgba(255, 255, 255, 0.3);
  color: white;
  transition: all 0.3s ease;
}

.browse-button:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-3px);
}

/* Floating Assistant Bubble */
.floating-assistant {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: white;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  padding: var(--spacing-md);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-sm);
  z-index: 1000;
  border: 1px solid var(--border-light);
  animation: float 3s ease-in-out infinite;
}

.assistant-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: var(--spacing-sm);
}

.assistant-title {
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--text);
}

.close-assistant {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  color: var(--text-light);
  transition: color 0.3s ease;
}

.close-assistant:hover {
  color: var(--text);
}

.assistant-message {
  font-size: 0.9rem;
  color: var(--text-light);
  text-align: center;
  margin-bottom: var(--spacing-sm);
}

.assistant-cta {
  width: 100%;
  font-weight: 700;
  font-size: 1rem;
  background: var(--gradient-primary) !important;
  border: none !important;
  border-radius: var(--radius-md);
  transition: all 0.3s ease;
}

.assistant-cta:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(99, 102, 241, 0.3);
}

@keyframes float {
  0% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
  100% {
    transform: translateY(0px);
  }
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-subtitle {
    font-size: 1.2rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .section-subtitle {
    font-size: 1.1rem;
  }
  
  .hero-search-container {
    margin: var(--spacing-lg);
  }
  
  .search-row {
    flex-direction: column;
  }
  
  .search-field {
    min-width: auto;
  }
  
  .search-actions {
    flex-direction: column;
    align-items: center;
  }
  
  .search-cta,
  .explore-button {
    min-width: auto;
    width: 100%;
  }
  
  .hero-actions,
  .cta-actions {
    flex-direction: column;
    align-items: center;
  }
  
  .steps-grid,
  .features-grid,
  .testimonials-grid,
  .trending-grid,
  .inspiration-grid,
  .trip-resume-grid {
    grid-template-columns: 1fr;
  }
  
  .cta-title {
    font-size: 2rem;
  }

  .floating-assistant {
    bottom: 10px;
    right: 10px;
  }
  
  .hero-content {
    padding: var(--spacing-xl);
    margin: var(--spacing-lg);
  }
  
  .trending-tags {
    flex-direction: column;
    gap: var(--spacing-xs);
  }
  
  .trending-details {
    flex-direction: column;
    gap: var(--spacing-xs);
  }
  
  .inspiration-filters {
    flex-direction: column;
    align-items: center;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .hero-subtitle {
    font-size: 1rem;
  }
  
  .section-title {
    font-size: 1.5rem;
  }
  

  
  .floating-assistant {
    bottom: 5px;
    right: 5px;
    left: 5px;
    width: auto;
  }
}
</style> 