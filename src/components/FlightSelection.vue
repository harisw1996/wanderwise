<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { AirplaneOutline, TimeOutline, CardOutline, StarOutline, SparklesOutline } from '@vicons/ionicons5'

const props = defineProps<{
  tripData: any
}>()

const emit = defineEmits<{
  update: [data: any]
  next: []
  prev: []
}>()

const selectedFlight = ref(props.tripData.selectedFlight || null)
const loading = ref(true)

const flights = ref([
  {
    id: 1,
    airline: 'Emirates',
    logo: '🇦🇪',
    price: '$1,250',
    duration: '14h 30m',
    stops: 'Direct',
    departure: '08:30',
    arrival: '22:00',
    rating: 4.8,
    features: ['Premium meals', 'Entertainment', 'WiFi'],
    recommendation: 'Best Overall',
    color: '#2C7BE5'
  },
  {
    id: 2,
    airline: 'Lufthansa',
    logo: '🇩🇪',
    price: '$890',
    duration: '16h 45m',
    stops: '1 stop',
    departure: '06:15',
    arrival: '19:00',
    rating: 4.6,
    features: ['Good value', 'Comfortable seats'],
    recommendation: 'Budget Pick',
    color: '#00C9A7'
  },
  {
    id: 3,
    airline: 'Singapore Airlines',
    logo: '🇸🇬',
    price: '$1,850',
    duration: '13h 15m',
    stops: 'Direct',
    departure: '23:50',
    arrival: '17:05',
    rating: 4.9,
    features: ['Luxury suites', 'Gourmet dining', 'Spa'],
    recommendation: 'Luxury Pick',
    color: '#FFC107'
  }
])

onMounted(() => {
  // Simulate loading
  setTimeout(() => {
    loading.value = false
  }, 1500)
})

const selectFlight = (flight: any) => {
  selectedFlight.value = flight
}

const handleNext = () => {
  if (selectedFlight.value) {
    emit('update', { selectedFlight: selectedFlight.value })
    emit('next')
  }
}
</script>

<template>
  <div class="flight-selection">
    <!-- Enhanced Header -->
    <div class="section-header">
      <div class="header-badge">
        <n-icon size="20" color="#2C7BE5">
          <AirplaneOutline />
        </n-icon>
        <span>AI-Recommended Flights</span>
      </div>
      
      <h2 class="section-title">
        Let's find the 
        <span class="title-highlight">best way</span> to get there
      </h2>
      
      <p class="section-subtitle">
        Smart recommendations for {{ tripData.destination }} based on your preferences
      </p>
    </div>

    <n-spin :show="loading" size="large">
      <div class="flights-container">
        <n-space vertical size="large">
          <n-card
            v-for="flight in flights"
            :key="flight.id"
            class="flight-card"
            :class="{ 'selected': selectedFlight?.id === flight.id }"
            hoverable
            @click="selectFlight(flight)"
          >
            <div class="flight-content">
              <!-- Enhanced Header -->
              <div class="flight-header">
                <div class="airline-info">
                  <div class="airline-logo" :style="{ backgroundColor: flight.color + '20' }">
                    <span class="logo-emoji">{{ flight.logo }}</span>
                  </div>
                  <div class="airline-details">
                    <h3 class="airline-name">{{ flight.airline }}</h3>
                    <n-tag v-if="flight.recommendation" :color="flight.color" size="small" class="recommendation-tag">
                      <template #icon>
                        <n-icon><SparklesOutline /></n-icon>
                      </template>
                      {{ flight.recommendation }}
                    </n-tag>
                  </div>
                </div>
                <div class="price-info">
                  <span class="price">{{ flight.price }}</span>
                  <span class="price-unit">per person</span>
                </div>
              </div>

              <!-- Enhanced Flight Details -->
              <div class="flight-details">
                <div class="time-info">
                  <div class="departure">
                    <span class="time">{{ flight.departure }}</span>
                    <span class="label">Departure</span>
                  </div>
                  <div class="duration">
                    <div class="duration-line">
                      <div class="line"></div>
                      <n-icon class="plane-icon"><AirplaneOutline /></n-icon>
                      <div class="line"></div>
                    </div>
                    <span class="duration-text">{{ flight.duration }}</span>
                    <span class="stops">{{ flight.stops }}</span>
                  </div>
                  <div class="arrival">
                    <span class="time">{{ flight.arrival }}</span>
                    <span class="label">Arrival</span>
                  </div>
                </div>

                <!-- Enhanced Features -->
                <div class="features">
                  <n-tag
                    v-for="feature in flight.features"
                    :key="feature"
                    size="small"
                    round
                    class="feature-tag"
                  >
                    {{ feature }}
                  </n-tag>
                </div>

                <!-- Enhanced Rating -->
                <div class="rating">
                  <div class="rating-stars">
                    <n-icon v-for="i in 5" :key="i" :color="i <= Math.floor(flight.rating) ? '#FFC107' : '#E9ECEF'">
                      <StarOutline />
                    </n-icon>
                  </div>
                  <span class="rating-text">{{ flight.rating }}/5</span>
                </div>
              </div>
            </div>
          </n-card>
        </n-space>
      </div>
    </n-spin>

    <!-- Enhanced Navigation -->
    <div class="navigation">
      <n-button @click="emit('prev')" size="large" class="nav-btn back-btn">
        ← Back to Trip Details
      </n-button>
      <n-button
        type="primary"
        :disabled="!selectedFlight"
        @click="handleNext"
        size="large"
        class="nav-btn continue-btn"
      >
        Continue to Hotels
        <template #icon>
          <n-icon><SparklesOutline /></n-icon>
        </template>
      </n-button>
    </div>
  </div>
</template>

<style scoped>
.flight-selection {
  max-width: 900px;
  margin: 0 auto;
  width: 100%;
}

.section-header {
  text-align: center;
  margin-bottom: var(--spacing-3xl);
}

.header-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-sm);
  background: rgba(44, 123, 229, 0.1);
  color: var(--primary);
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--radius-xl);
  font-weight: 600;
  font-size: 0.9rem;
  margin-bottom: var(--spacing-lg);
  border: 1px solid rgba(44, 123, 229, 0.2);
}

.section-title {
  font-size: 3rem;
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

.section-subtitle {
  font-size: 1.3rem;
  color: var(--text-light);
  margin: 0;
  line-height: 1.6;
}

.flights-container {
  margin-bottom: var(--spacing-3xl);
}

.flight-card {
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 2px solid var(--border-light);
  border-radius: var(--radius-lg);
  background: var(--card-bg);
  box-shadow: var(--shadow-card);
}

.flight-card:hover {
  transform: translateY(-6px);
  box-shadow: var(--shadow-card-hover);
  border-color: var(--primary-light);
}

.flight-card.selected {
  border-color: var(--primary);
  box-shadow: 0 0 0 4px rgba(44, 123, 229, 0.1);
  transform: translateY(-6px);
}

.flight-content {
  padding: var(--spacing-xl);
}

.flight-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--spacing-xl);
}

.airline-info {
  display: flex;
  align-items: center;
  gap: var(--spacing-lg);
}

.airline-logo {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 64px;
  height: 64px;
  border-radius: var(--radius-lg);
  border: 2px solid var(--border-light);
}

.logo-emoji {
  font-size: 2.5rem;
}

.airline-details {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);
}

.airline-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0;
  color: var(--text);
}

.recommendation-tag {
  font-weight: 600;
  border-radius: var(--radius-md);
}

.price-info {
  text-align: right;
}

.price {
  font-size: 2.5rem;
  font-weight: 800;
  color: var(--primary);
  display: block;
  line-height: 1;
}

.price-unit {
  font-size: 1rem;
  color: var(--text-light);
  font-weight: 500;
}

.flight-details {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xl);
}

.time-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--spacing-xl);
  background: var(--background);
  border-radius: var(--radius-lg);
  border: 1px solid var(--border-light);
}

.departure, .arrival {
  text-align: center;
  flex: 1;
}

.time {
  font-size: 2rem;
  font-weight: 700;
  display: block;
  color: var(--text);
}

.label {
  font-size: 1rem;
  color: var(--text-light);
  font-weight: 500;
  margin-top: var(--spacing-xs);
}

.duration {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-md);
  flex: 2;
}

.duration-line {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  width: 100%;
  max-width: 200px;
}

.line {
  flex: 1;
  height: 2px;
  background: var(--gradient-primary);
  border-radius: 1px;
}

.plane-icon {
  color: var(--primary);
  font-size: 1.2rem;
}

.duration-text {
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--text);
}

.stops {
  font-size: 0.9rem;
  color: var(--text-light);
  background: var(--background-alt);
  padding: var(--spacing-xs) var(--spacing-sm);
  border-radius: var(--radius-md);
  font-weight: 500;
}

.features {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-md);
}

.feature-tag {
  background: var(--background-alt);
  border: 1px solid var(--border-light);
  color: var(--text);
  font-weight: 500;
}

.rating {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--spacing-md);
  background: var(--background-alt);
  border-radius: var(--radius-md);
  border: 1px solid var(--border-light);
}

.rating-stars {
  display: flex;
  gap: var(--spacing-xs);
}

.rating-text {
  font-weight: 600;
  color: var(--text);
  font-size: 1rem;
}

.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: var(--spacing-lg);
}

.nav-btn {
  padding: var(--spacing-md) var(--spacing-xl);
  font-weight: 600;
  border-radius: var(--radius-lg);
  transition: all 0.3s ease;
}

.back-btn {
  background: var(--background-alt);
  border: 2px solid var(--border-light);
  color: var(--text);
}

.back-btn:hover {
  background: var(--background);
  border-color: var(--primary-light);
  transform: translateY(-2px);
}

.continue-btn {
  background: var(--gradient-primary) !important;
  border: none !important;
  color: white;
}

.continue-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 12px 35px rgba(44, 123, 229, 0.4);
}

.continue-btn:disabled {
  opacity: 0.6;
  transform: none;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.2rem;
  }
  
  .section-subtitle {
    font-size: 1.1rem;
  }
  
  .flight-header {
    flex-direction: column;
    gap: var(--spacing-lg);
  }
  
  .price-info {
    text-align: left;
  }
  
  .time-info {
    flex-direction: column;
    gap: var(--spacing-lg);
  }
  
  .navigation {
    flex-direction: column;
    gap: var(--spacing-md);
  }
  
  .nav-btn {
    width: 100%;
  }
}
</style>