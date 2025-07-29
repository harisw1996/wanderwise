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
  CloseOutline
} from '@vicons/ionicons5'

const emit = defineEmits<{
  startPlanning: []
}>()



// Floating assistant
const showAssistant = ref(true)

const destinations = [
  { 
    name: 'Kyoto', 
    image: 'https://images.unsplash.com/photo-1545569341-9eb8b30979d9?w=400&h=300&fit=crop', 
    country: 'Japan',
    tags: ['🏛️ Culture', '🍁 Nature'],
    weather: '🌤️ 22°C',
    priceRange: '$800-1200'
  },
  { 
    name: 'Santorini', 
    image: 'https://images.unsplash.com/photo-1570077188670-e3a8d69ac5ff?w=400&h=300&fit=crop', 
    country: 'Greece',
    tags: ['🏝️ Beach', '🥘 Food'],
    weather: '☀️ 28°C',
    priceRange: '$1000-1500'
  },
  { 
    name: 'Banff', 
    image: 'https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=400&h=300&fit=crop', 
    country: 'Canada',
    tags: ['🏔️ Adventure', '🍁 Nature'],
    weather: '❄️ 5°C',
    priceRange: '$600-900'
  },
  { 
    name: 'Bali', 
    image: 'https://images.unsplash.com/photo-1537953773345-d172ccf13cf1?w=400&h=300&fit=crop', 
    country: 'Indonesia',
    tags: ['🏝️ Beach', '🧘 Relaxation'],
    weather: '🌤️ 30°C',
    priceRange: '$500-800'
  },
  { 
    name: 'Paris', 
    image: 'https://images.unsplash.com/photo-1502602898535-0e2b9b2b7b1a?w=400&h=300&fit=crop', 
    country: 'France',
    tags: ['🏛️ Culture', '🥘 Food'],
    weather: '🌤️ 18°C',
    priceRange: '$900-1400'
  },
  { 
    name: 'Machu Picchu', 
    image: 'https://images.unsplash.com/photo-1587595431973-160d0d94add1?w=400&h=300&fit=crop', 
    country: 'Peru',
    tags: ['🏔️ Adventure', '🏛️ Culture'],
    weather: '🌤️ 15°C',
    priceRange: '$700-1100'
  }
]

const testimonials = [
  {
    quote: "Wanderwise made my honeymoon stress-free! The AI suggested perfect restaurants and activities we never would have found.",
    author: "🇺🇸 Sarah & Mike",
    trip: "Paris Honeymoon",
    avatar: "https://images.unsplash.com/photo-1494790108755-2616b612b786?w=60&h=60&fit=crop&crop=face"
  },
  {
    quote: "I planned a 10-day trip to Japan in 5 minutes. The itinerary was perfect and included hidden gems.",
    author: "🇨🇦 Alex Chen",
    trip: "Japan Adventure",
    avatar: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=60&h=60&fit=crop&crop=face"
  },
  {
    quote: "The weather predictions were spot-on and helped us pack perfectly. No more overpacking!",
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
  { icon: LocationOutline, label: "Intent & Dates", description: "Tell us where and when" },
  { icon: AirplaneOutline, label: "Flights", description: "AI finds the best routes" },
  { icon: BedOutline, label: "Hotels", description: "Perfect accommodations" },
  { icon: SunnyOutline, label: "Weather", description: "Smart packing guidance" },
  { icon: MapOutline, label: "Itinerary", description: "Daily plans & activities" },
  { icon: CheckmarkCircleOutline, label: "Final Review", description: "Perfect your trip" }
]

const handleStartPlanning = () => {
  emit('startPlanning')
}



const closeAssistant = () => {
  showAssistant.value = false
}
</script>

<template>
  <div class="homepage">
    <!-- Hero Section -->
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
            Discover Your Next Adventure
            <span class="title-highlight">Planned Intelligently with AI</span>
          </h1>
          
          <p class="hero-subtitle">
            Tell us where, when, and how — Wanderwise handles the rest.
          </p>
        </div>
        
        <div class="hero-actions">
          <n-button 
            type="primary" 
            size="large" 
            class="cta-button"
            @click="handleStartPlanning"
          >
            <template #icon>
              <n-icon><SparklesOutline /></n-icon>
            </template>
            Plan My Trip
          </n-button>
          
          <n-button 
            size="large" 
            class="demo-button"
            ghost
          >
            Explore Ideas
          </n-button>
        </div>
        
        <!-- Scroll indicator -->
        <div class="scroll-indicator">
          <span>↓ Scroll to begin</span>
        </div>
      </div>
    </section>



    <!-- How It Works Section -->
    <section class="how-it-works">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Your Trip in 6 Smart Steps</h2>
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
          <h2 class="section-title">Why Choose Wanderwise?</h2>
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

    <!-- Destination Gallery Section -->
    <section class="destination-gallery">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Popular Destinations</h2>
          <p class="section-subtitle">Get inspired by these amazing places and start planning your next adventure.</p>
        </div>
        
        <div class="destinations-grid">
          <div 
            v-for="destination in destinations" 
            :key="destination.name"
            class="destination-card"
          >
            <div class="destination-image">
              <img 
                :src="destination.image" 
                :alt="destination.name"
                @error="$event.target.src='https://picsum.photos/400/300?random=100'"
                loading="lazy"
              />
              <div class="destination-tags">
                <span 
                  v-for="tag in destination.tags" 
                  :key="tag"
                  class="destination-tag"
                >
                  {{ tag }}
                </span>
              </div>
              <div class="destination-overlay">
                <div class="destination-info">
                  <h3 class="destination-name">{{ destination.name }}</h3>
                  <p class="destination-country">{{ destination.country }}</p>
                  <div class="destination-details">
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
          <span class="assistant-title">💬 Need help planning?</span>
          <button class="close-assistant" @click="closeAssistant">
            <n-icon size="16">
              <CloseOutline />
            </n-icon>
          </button>
        </div>
        <p class="assistant-message">I can suggest ideas or help you resume previous planning!</p>
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

.hero-actions {
  display: flex;
  gap: var(--spacing-lg);
  justify-content: center;
  flex-wrap: wrap;
}

.cta-button {
  height: 56px;
  font-weight: 700;
  font-size: 1.1rem;
  background: var(--gradient-primary) !important;
  border: none !important;
  border-radius: var(--radius-lg);
  transition: all 0.3s ease;
}

.cta-button:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 12px 35px rgba(99, 102, 241, 0.4);
}

.demo-button {
  height: 56px;
  font-weight: 600;
  font-size: 1.1rem;
  border-radius: var(--radius-lg);
  border: 2px solid rgba(255, 255, 255, 0.3);
  color: white;
  transition: all 0.3s ease;
}

.demo-button:hover {
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

/* How It Works Section */
.how-it-works {
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

/* Destination Gallery Section */
.destination-gallery {
  padding: var(--spacing-3xl) 0;
  background: white;
}

.destinations-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-lg);
}

.destination-card {
  border-radius: var(--radius-xl);
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  cursor: pointer;
}

.destination-card:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.destination-image {
  position: relative;
  height: 250px;
  overflow: hidden;
  background: transparent;
}

.destination-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.destination-card:hover .destination-image img {
  transform: scale(1.1);
}

.destination-tags {
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

.destination-tag {
  font-size: 0.7rem;
  font-weight: 600;
  color: white;
  background: var(--gradient-primary);
  border-radius: var(--radius-sm);
  padding: var(--spacing-xs) var(--spacing-sm);
  white-space: nowrap;
}

.destination-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  color: white;
  padding: var(--spacing-lg);
  z-index: 2;
}

.destination-info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.destination-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0 0 var(--spacing-xs) 0;
}

.destination-country {
  margin: 0;
  opacity: 0.9;
}

.destination-details {
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
  
  .hero-actions,
  .cta-actions {
    flex-direction: column;
    align-items: center;
  }
  
  .steps-grid,
  .features-grid,
  .testimonials-grid,
  .destinations-grid {
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
  
  .destination-tags {
    flex-direction: column;
    gap: var(--spacing-xs);
  }
  
  .destination-details {
    flex-direction: column;
    gap: var(--spacing-xs);
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