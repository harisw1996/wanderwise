<script setup lang="ts">
import { ref, computed } from 'vue'
import { darkTheme, lightTheme } from 'naive-ui'
import type { GlobalThemeOverrides } from 'naive-ui'
import Header from './components/Header.vue'
import HeroSearch from './components/HeroSearch.vue'
import FlightSelection from './components/FlightSelection.vue'
import AccommodationSelection from './components/AccommodationSelection.vue'
import WeatherInfo from './components/WeatherInfo.vue'
import ItineraryBuilder from './components/ItineraryBuilder.vue'
import TripSummary from './components/TripSummary.vue'
import Footer from './components/Footer.vue'

const currentStep = ref(1)
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
    primaryColor: '#2C7BE5',
    primaryColorHover: '#1c6ed4',
    primaryColorPressed: '#0b5cc7',
    successColor: '#00C9A7',
    warningColor: '#FFC107',
    errorColor: '#DC3545',
    fontFamily: 'Inter, system-ui, -apple-system, sans-serif'
  },
  Card: {
    borderRadius: '12px'
  },
  Button: {
    borderRadius: '8px'
  }
}

const steps = [
  { number: 1, title: 'Trip Details', component: 'HeroSearch' },
  { number: 2, title: 'Flights', component: 'FlightSelection' },
  { number: 3, title: 'Hotels', component: 'AccommodationSelection' },
  { number: 4, title: 'Weather', component: 'WeatherInfo' },
  { number: 5, title: 'Itinerary', component: 'ItineraryBuilder' },
  { number: 6, title: 'Summary', component: 'TripSummary' }
]

const currentComponent = computed(() => {
  const step = steps.find(s => s.number === currentStep.value)
  return step?.component || 'HeroSearch'
})

const canProceed = computed(() => {
  switch (currentStep.value) {
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
  if (currentStep.value > 1) {
    currentStep.value--
  }
}

const skipStep = () => {
  if (currentStep.value < 6) {
    currentStep.value++
  }
}

const updateTripData = (data: any) => {
  tripData.value = { ...tripData.value, ...data }
}
</script>

<template>
  <n-config-provider :theme="lightTheme" :theme-overrides="themeOverrides">
    <n-message-provider>
      <div class="app">
        <Header />
        
        <!-- Progress Steps -->
        <div class="container" style="margin-top: 24px;">
          <n-steps :current="currentStep" size="small">
            <n-step 
              v-for="step in steps" 
              :key="step.number"
              :title="step.title"
            />
          </n-steps>
        </div>

        <!-- Main Content -->
        <main class="main-content">
          <div class="container">
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
}

.main-content {
  flex: 1;
  padding: var(--spacing-2xl) 0;
}

.step-content {
  min-height: 500px;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateX(20px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateX(-20px);
}
</style>