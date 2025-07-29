<script setup lang="ts">
import { ref, computed } from 'vue'
import { darkTheme, lightTheme } from 'naive-ui'
import type { GlobalThemeOverrides } from 'naive-ui'
import Header from './components/Header.vue'
import Homepage from './components/Homepage.vue'
import HeroSearch from './components/HeroSearch.vue'
import FlightSelection from './components/FlightSelection.vue'
import AccommodationSelection from './components/AccommodationSelection.vue'
import WeatherInfo from './components/WeatherInfo.vue'
import ItineraryBuilder from './components/ItineraryBuilder.vue'
import TripSummary from './components/TripSummary.vue'
import Footer from './components/Footer.vue'

const currentStep = ref(0)
const tripData = ref({
  destination: '',
  dates: null as [number, number] | null,
  tripType: '',
  budget: '',
  selectedFlight: null,
  selectedHotel: null,
  preferences: {
    food: [] as string[],
    interests: [] as string[],
    pace: ''
  },
  itinerary: [] as any[]
})

const themeOverrides: GlobalThemeOverrides = {
  common: {
    primaryColor: '#6366F1',
    primaryColorHover: '#4F46E5',
    primaryColorPressed: '#3730A3',
    successColor: '#10B981',
    warningColor: '#F59E0B',
    errorColor: '#EF4444',
    fontFamily: 'Inter, system-ui, -apple-system, sans-serif'
  },
  Card: {
    borderRadius: '16px'
  },
  Button: {
    borderRadius: '12px'
  },
  Steps: {
    stepHeaderFontSize: '16px',
    stepDescriptionFontSize: '14px'
  }
}

const steps = [
  { number: 0, title: 'Home', component: 'Homepage' },
  { number: 1, title: 'Trip Details', component: 'HeroSearch' },
  { number: 2, title: 'Flights', component: 'FlightSelection' },
  { number: 3, title: 'Hotels', component: 'AccommodationSelection' },
  { number: 4, title: 'Weather', component: 'WeatherInfo' },
  { number: 5, title: 'Itinerary', component: 'ItineraryBuilder' },
  { number: 6, title: 'Summary', component: 'TripSummary' }
]

const currentComponent = computed(() => {
  const step = steps.find(s => s.number === currentStep.value)
  return step?.component || 'Homepage'
})

const canProceed = computed(() => {
  switch (currentStep.value) {
    case 0:
      return true // Homepage can always proceed
    case 1:
      return tripData.value.destination && tripData.value.dates && tripData.value.tripType
    case 2:
      return tripData.value.selectedFlight
    case 3:
      return tripData.value.selectedHotel
    case 4:
      return true // Weather is just informational
    case 5:
      return true // Itinerary can be skipped
    default:
      return true
  }
})

const nextStep = () => {
  if (currentStep.value < 6 && canProceed.value) {
    currentStep.value++
  }
}

const prevStep = () => {
  if (currentStep.value > 0) {
    currentStep.value--
  }
}

const skipStep = () => {
  if (currentStep.value < 6) {
    currentStep.value++
  }
}

const startPlanning = () => {
  currentStep.value = 1
}

const updateTripData = (data: any) => {
  tripData.value = { ...tripData.value, ...data }
}

const getStepDescription = (stepNumber: number) => {
  const descriptions = {
    0: 'Welcome to Wanderwise',
    1: 'Tell us about your dream trip',
    2: 'Find the perfect flights',
    3: 'Choose your accommodation',
    4: 'Check the weather forecast',
    5: 'Build your itinerary',
    6: 'Review and save your trip'
  }
  return descriptions[stepNumber as keyof typeof descriptions] || ''
}
</script>

<template>
  <n-config-provider :theme="lightTheme" :theme-overrides="themeOverrides">
    <n-message-provider>
      <div class="app">
        <Header />
        
        <!-- Enhanced Progress Steps (hidden on homepage) -->
        <div v-if="currentStep > 0" class="progress-section">
          <div class="container">
            <div class="progress-wrapper">
              <n-steps :current="currentStep" size="medium" class="enhanced-steps">
                <n-step 
                  v-for="step in steps.filter(s => s.number > 0)" 
                  :key="step.number"
                  :title="step.title"
                  :description="getStepDescription(step.number)"
                />
              </n-steps>
            </div>
          </div>
        </div>

        <!-- Enhanced Main Content -->
        <main class="main-content">
          <div v-if="currentStep === 0" class="homepage-container">
            <Homepage @startPlanning="startPlanning" />
          </div>
          <div v-else class="container">
            <Transition name="fade" mode="out-in">
              <div :key="currentStep" class="step-content fade-in">
                <HeroSearch 
                  v-if="currentComponent === 'HeroSearch'"
                  :trip-data="tripData"
                  @update="updateTripData"
                  @next="nextStep"
                />
                <FlightSelection 
                  v-else-if="currentComponent === 'FlightSelection'"
                  :trip-data="tripData"
                  @update="updateTripData"
                  @next="nextStep"
                  @prev="prevStep"
                />
                <AccommodationSelection 
                  v-else-if="currentComponent === 'AccommodationSelection'"
                  :trip-data="tripData"
                  @update="updateTripData"
                  @next="nextStep"
                  @prev="prevStep"
                />
                <WeatherInfo 
                  v-else-if="currentComponent === 'WeatherInfo'"
                  :trip-data="tripData"
                  @next="nextStep"
                  @prev="prevStep"
                  @skip="skipStep"
                />
                <ItineraryBuilder 
                  v-else-if="currentComponent === 'ItineraryBuilder'"
                  :trip-data="tripData"
                  @update="updateTripData"
                  @next="nextStep"
                  @prev="prevStep"
                  @skip="skipStep"
                />
                <TripSummary 
                  v-else-if="currentComponent === 'TripSummary'"
                  :trip-data="tripData"
                  @prev="prevStep"
                />
              </div>
            </Transition>
          </div>
        </main>

        <Footer />
      </div>
    </n-message-provider>
  </n-config-provider>
</template>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: var(--background);
}

.progress-section {
  background: var(--background-alt);
  border-bottom: 1px solid var(--border-light);
  padding: var(--spacing-lg) 0;
  position: sticky;
  top: 72px;
  z-index: 50;
  backdrop-filter: blur(10px);
}

.progress-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

.enhanced-steps {
  max-width: 800px;
  width: 100%;
}

.enhanced-steps :deep(.n-step) {
  padding: 0 var(--spacing-md);
}

.enhanced-steps :deep(.n-step-splitor) {
  background: var(--border-light);
}

.enhanced-steps :deep(.n-step-splitor--active) {
  background: var(--gradient-primary);
}

.enhanced-steps :deep(.n-step-indicator) {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  font-weight: 600;
  font-size: 16px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: var(--shadow-card);
}

.enhanced-steps :deep(.n-step-indicator--process) {
  background: var(--gradient-primary);
  color: white;
  box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.2);
}

.enhanced-steps :deep(.n-step-indicator--finish) {
  background: var(--gradient-primary);
  color: white;
  transform: scale(1.1);
}

.enhanced-steps :deep(.n-step-indicator--wait) {
  background: var(--background-alt);
  color: var(--text-light);
  border: 2px solid var(--border);
}

.enhanced-steps :deep(.n-step-content) {
  margin-top: var(--spacing-sm);
}

.enhanced-steps :deep(.n-step-content__title) {
  font-weight: 600;
  color: var(--text);
  font-size: 14px;
}

.enhanced-steps :deep(.n-step-content__description) {
  color: var(--text-light);
  font-size: 12px;
  margin-top: 2px;
}

.main-content {
  flex: 1;
  min-height: calc(100vh - 200px);
}

.homepage-container {
  padding: 0;
  min-height: 100vh;
}

.step-content {
  min-height: 600px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-2xl) 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.fade-enter-from {
  opacity: 0;
  transform: translateX(30px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

@media (max-width: 768px) {
  .progress-section {
    padding: var(--spacing-md) 0;
  }
  
  .enhanced-steps :deep(.n-step) {
    padding: 0 var(--spacing-sm);
  }
  
  .enhanced-steps :deep(.n-step-indicator) {
    width: 40px;
    height: 40px;
    font-size: 14px;
  }
  
  .enhanced-steps :deep(.n-step-content__title) {
    font-size: 12px;
  }
  
  .enhanced-steps :deep(.n-step-content__description) {
    font-size: 10px;
  }
}
</style>