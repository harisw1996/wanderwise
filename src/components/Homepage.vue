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
  ArrowForwardOutline
} from '@vicons/ionicons5'

const emit = defineEmits<{
  startPlanning: []
}>()

const destinations = [
  { name: 'Kyoto', image: 'https://picsum.photos/400/300?random=1', country: 'Japan' },
  { name: 'Santorini', image: 'https://picsum.photos/400/300?random=2', country: 'Greece' },
  { name: 'Banff', image: 'https://picsum.photos/400/300?random=3', country: 'Canada' },
  { name: 'Bali', image: 'https://picsum.photos/400/300?random=4', country: 'Indonesia' },
  { name: 'Paris', image: 'https://picsum.photos/400/300?random=5', country: 'France' },
  { name: 'Machu Picchu', image: 'https://picsum.photos/400/300?random=6', country: 'Peru' }
]

const testimonials = [
  {
    quote: "Wanderwise made my honeymoon stress-free! The AI suggested perfect restaurants and activities we never would have found.",
    author: "Sarah & Mike",
    trip: "Paris Honeymoon",
    avatar: "https://picsum.photos/60/60?random=10"
  },
  {
    quote: "I planned a 10-day trip to Japan in 5 minutes. The itinerary was perfect and included hidden gems.",
    author: "Alex Chen",
    trip: "Japan Adventure",
    avatar: "https://picsum.photos/60/60?random=11"
  },
  {
    quote: "The weather predictions were spot-on and helped us pack perfectly. No more overpacking!",
    author: "Maria Rodriguez",
    trip: "Bali Family Trip",
    avatar: "https://picsum.photos/60/60?random=12"
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
          <span>AI-Powered Travel Planning</span>
        </div>
        
        <h1 class="hero-title">
          Your Dream Trip, 
          <span class="title-highlight">Designed by AI</span>
        </h1>
        
        <p class="hero-subtitle">
          Tell us where, when, and how — Wanderwise handles the rest.
        </p>
        
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
            Start Planning
          </n-button>
          
          <n-button 
            size="large" 
            class="demo-button"
            ghost
          >
            Try Sample Trip
          </n-button>
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
            v-for="testimonial in testimonials" 
            :key="testimonial.author"
            class="testimonial-card"
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
              <div class="destination-overlay">
                <h3 class="destination-name">{{ destination.name }}</h3>
                <p class="destination-country">{{ destination.country }}</p>
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
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.7) 0%, rgba(118, 75, 162, 0.8) 100%);
  z-index: 1;
}

.hero-content {
  max-width: 800px;
  padding: 0 var(--spacing-lg);
  z-index: 2;
  position: relative;
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
  transform: translateY(-3px);
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
  transform: translateY(-3px);
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
  box-shadow: var(--shadow-card);
  transition: all 0.3s ease;
  border: 1px solid var(--border-light);
}

.step-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-card-hover);
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
  box-shadow: var(--shadow-card);
  transition: all 0.3s ease;
  border: 1px solid var(--border-light);
}

.testimonial-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-card-hover);
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
  box-shadow: var(--shadow-card);
  transition: all 0.3s ease;
  cursor: pointer;
}

.destination-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-card-hover);
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

.destination-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  color: white;
  padding: var(--spacing-lg);
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
}
</style> 