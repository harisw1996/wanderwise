<script setup lang="ts">
import { ref, computed } from 'vue'
import { LocationOutline, CalendarOutline, PeopleOutline, CardOutline, SparklesOutline } from '@vicons/ionicons5'

const props = defineProps<{
  tripData: any
}>()

const emit = defineEmits<{
  update: [data: any]
  next: []
}>()

const destination = ref(props.tripData.destination || '')
const dateRange = ref<[number, number] | null>(props.tripData.dates || null)
const tripType = ref(props.tripData.tripType || '')
const budget = ref(props.tripData.budget || '')

const tripTypes = [
  { label: '🧑‍💼 Solo Adventure', value: 'solo' },
  { label: '👨‍👩‍👧‍👦 Family Fun', value: 'family' },
  { label: '💼 Business Trip', value: 'business' },
  { label: '🙏 Spiritual Journey', value: 'spiritual' },
  { label: '💕 Honeymoon', value: 'honeymoon' },
  { label: '👥 Friends Getaway', value: 'friends' }
]

const budgetOptions = [
  { label: '💸 Budget-friendly ($500-1500)', value: 'budget' },
  { label: '🏨 Mid-range ($1500-3000)', value: 'mid' },
  { label: '✨ Luxury ($3000+)', value: 'luxury' },
  { label: '🤷‍♂️ I\'m flexible', value: 'flexible' }
]

const canProceed = computed(() => {
  return destination.value && dateRange.value && tripType.value
})

const handleNext = () => {
  if (canProceed.value) {
    emit('update', {
      destination: destination.value,
      dates: dateRange.value,
      tripType: tripType.value,
      budget: budget.value
    })
    emit('next')
  }
}

const destinationOptions = [
  'Paris, France',
  'Tokyo, Japan',
  'New York, USA',
  'Bali, Indonesia',
  'Rome, Italy',
  'Bangkok, Thailand',
  'London, UK',
  'Dubai, UAE'
]
</script>

<template>
  <div class="hero-search">
    <!-- Background Elements -->
    <div class="hero-background">
      <div class="floating-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
        <div class="shape shape-4"></div>
      </div>
    </div>

    <div class="hero-content">
      <!-- Enhanced Header -->
      <div class="hero-header">
        <div class="hero-badge">
          <n-icon size="20" color="#00C9A7">
            <SparklesOutline />
          </n-icon>
          <span>AI-Powered Travel Planning</span>
        </div>
        
        <h1 class="hero-title">
          Where to 
          <span class="title-highlight">next?</span>
        </h1>
        
        <p class="hero-subtitle">
          Let's plan your perfect trip with intelligent recommendations and personalized experiences
        </p>
      </div>

      <!-- Enhanced Search Card -->
      <n-card class="search-card" size="large">
        <div class="card-header">
          <h3 class="card-title">Plan Your Dream Trip</h3>
          <p class="card-subtitle">Tell us about your adventure and we'll create the perfect itinerary</p>
        </div>

        <n-space vertical size="large">
          <!-- Destination -->
          <div class="input-group">
            <label class="input-label">
              <div class="label-icon">
                <n-icon><LocationOutline /></n-icon>
              </div>
              <span>Where do you want to go?</span>
            </label>
            <n-auto-complete
              v-model:value="destination"
              :options="destinationOptions.map(d => ({ label: d, value: d }))"
              placeholder="Enter your dream destination..."
              size="large"
              clearable
              class="enhanced-input"
            />
          </div>

          <!-- Date Range -->
          <div class="input-group">
            <label class="input-label">
              <div class="label-icon">
                <n-icon><CalendarOutline /></n-icon>
              </div>
              <span>When are you traveling?</span>
            </label>
            <n-date-picker
              v-model:value="dateRange"
              type="daterange"
              size="large"
              placeholder="Select your travel dates"
              style="width: 100%"
              class="enhanced-input"
            />
          </div>

          <!-- Trip Type -->
          <div class="input-group">
            <label class="input-label">
              <div class="label-icon">
                <n-icon><PeopleOutline /></n-icon>
              </div>
              <span>What type of trip is this?</span>
            </label>
            <n-select
              v-model:value="tripType"
              :options="tripTypes"
              placeholder="Choose your trip style"
              size="large"
              class="enhanced-input"
            />
          </div>

          <!-- Budget (Optional) -->
          <div class="input-group">
            <label class="input-label">
              <div class="label-icon">
                <n-icon><CardOutline /></n-icon>
              </div>
              <span>What's your budget? <span class="optional-text">(Optional)</span></span>
            </label>
            <n-select
              v-model:value="budget"
              :options="budgetOptions"
              placeholder="Select your budget range"
              size="large"
              clearable
              class="enhanced-input"
            />
          </div>

          <!-- Enhanced Action Button -->
          <div class="action-section">
            <n-button
              type="primary"
              size="large"
              :disabled="!canProceed"
              @click="handleNext"
              class="cta-button"
            >
              <template #icon>
                <n-icon><SparklesOutline /></n-icon>
              </template>
              Start Planning My Trip
            </n-button>
            
            <div class="features-preview">
              <div class="feature-item">
                <n-icon size="16" color="#00C9A7">
                  <SparklesOutline />
                </n-icon>
                <span>AI Recommendations</span>
              </div>
              <div class="feature-item">
                <n-icon size="16" color="#2C7BE5">
                  <CalendarOutline />
                </n-icon>
                <span>Smart Itineraries</span>
              </div>
              <div class="feature-item">
                <n-icon size="16" color="#FFC107">
                  <LocationOutline />
                </n-icon>
                <span>Local Insights</span>
              </div>
            </div>
          </div>
        </n-space>
      </n-card>
    </div>
  </div>
</template>

<style scoped>
.hero-search {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-2xl) 0;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--gradient-hero);
  z-index: -1;
}

.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(44, 123, 229, 0.1), rgba(0, 201, 167, 0.1));
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 80px;
  height: 80px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 120px;
  height: 120px;
  top: 60%;
  right: 15%;
  animation-delay: 2s;
}

.shape-3 {
  width: 60px;
  height: 60px;
  top: 80%;
  left: 20%;
  animation-delay: 4s;
}

.shape-4 {
  width: 100px;
  height: 100px;
  top: 30%;
  right: 30%;
  animation-delay: 1s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

.hero-content {
  max-width: 700px;
  width: 100%;
  text-align: center;
  z-index: 1;
}

.hero-header {
  margin-bottom: var(--spacing-3xl);
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-sm);
  background: rgba(0, 201, 167, 0.1);
  color: var(--accent-1);
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--radius-xl);
  font-weight: 600;
  font-size: 0.9rem;
  margin-bottom: var(--spacing-lg);
  border: 1px solid rgba(0, 201, 167, 0.2);
}

.hero-title {
  font-size: 4rem;
  font-weight: 800;
  color: var(--text);
  margin: 0 0 var(--spacing-md) 0;
  line-height: 1.1;
  letter-spacing: -1px;
}

.title-highlight {
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.4rem;
  color: var(--text-light);
  margin: 0;
  line-height: 1.6;
  max-width: 600px;
  margin: 0 auto;
}

.search-card {
  text-align: left;
  box-shadow: var(--shadow-card-hover);
  border: 0;
  border-radius: var(--radius-xl);
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.card-header {
  text-align: center;
  margin-bottom: var(--spacing-xl);
}

.card-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-sm) 0;
}

.card-subtitle {
  color: var(--text-light);
  margin: 0;
  font-size: 1rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.input-label {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
  font-weight: 600;
  color: var(--text);
  font-size: 1rem;
}

.label-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background: var(--gradient-primary);
  border-radius: var(--radius-md);
  color: white;
}

.optional-text {
  color: var(--text-lighter);
  font-weight: 400;
  font-size: 0.9rem;
}

.enhanced-input :deep(.n-input) {
  border-radius: var(--radius-md);
  border: 2px solid var(--border-light);
  transition: all 0.3s ease;
}

.enhanced-input :deep(.n-input:hover) {
  border-color: var(--primary-light);
}

.enhanced-input :deep(.n-input--focus) {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(44, 123, 229, 0.1);
}

.action-section {
  margin-top: var(--spacing-xl);
  text-align: center;
}

.cta-button {
  width: 100%;
  height: 56px;
  font-weight: 700;
  font-size: 1.1rem;
  background: var(--gradient-primary) !important;
  border: none !important;
  border-radius: var(--radius-lg);
  transition: all 0.3s ease;
  margin-bottom: var(--spacing-lg);
}

.cta-button:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 12px 35px rgba(44, 123, 229, 0.4);
}

.cta-button:disabled {
  opacity: 0.6;
  transform: none;
}

.features-preview {
  display: flex;
  justify-content: center;
  gap: var(--spacing-xl);
  flex-wrap: wrap;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  font-size: 0.9rem;
  color: var(--text-light);
  font-weight: 500;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2.8rem;
  }
  
  .hero-subtitle {
    font-size: 1.2rem;
  }
  
  .features-preview {
    flex-direction: column;
    gap: var(--spacing-md);
  }
  
  .shape {
    display: none;
  }
}
</style>