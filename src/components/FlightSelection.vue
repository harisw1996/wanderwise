<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { AirplaneOutline, TimeOutline, CardOutline, StarOutline } from '@vicons/ionicons5'

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
    recommendation: 'Best Overall'
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
    recommendation: 'Budget Pick'
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
    recommendation: 'Luxury Pick'
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
    <div class="section-header">
      <h2 class="section-title">Let's find the best way to get there</h2>
      <p class="section-subtitle">
        AI-recommended flights to {{ tripData.destination }}
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
              <!-- Header -->
              <div class="flight-header">
                <div class="airline-info">
                  <span class="airline-logo">{{ flight.logo }}</span>
                  <div>
                    <h3 class="airline-name">{{ flight.airline }}</h3>
                    <n-tag v-if="flight.recommendation" type="success" size="small">
                      {{ flight.recommendation }}
                    </n-tag>
                  </div>
                </div>
                <div class="price-info">
                  <span class="price">{{ flight.price }}</span>
                  <span class="price-unit">per person</span>
                </div>
              </div>

              <!-- Flight Details -->
              <div class="flight-details">
                <div class="time-info">
                  <div class="departure">
                    <span class="time">{{ flight.departure }}</span>
                    <span class="label">Departure</span>
                  </div>
                  <div class="duration">
                    <n-icon><AirplaneOutline /></n-icon>
                    <span>{{ flight.duration }}</span>
                    <span class="stops">{{ flight.stops }}</span>
                  </div>
                  <div class="arrival">
                    <span class="time">{{ flight.arrival }}</span>
                    <span class="label">Arrival</span>
                  </div>
                </div>

                <!-- Features -->
                <div class="features">
                  <n-tag
                    v-for="feature in flight.features"
                    :key="feature"
                    size="small"
                    round
                  >
                    {{ feature }}
                  </n-tag>
                </div>

                <!-- Rating -->
                <div class="rating">
                  <n-icon color="#FFC107"><StarOutline /></n-icon>
                  <span>{{ flight.rating }}</span>
                </div>
              </div>
            </div>
          </n-card>
        </n-space>
      </div>
    </n-spin>

    <!-- Navigation -->
    <div class="navigation">
      <n-button @click="emit('prev')" size="large">
        ← Back
      </n-button>
      <n-button
        type="primary"
        :disabled="!selectedFlight"
        @click="handleNext"
        size="large"
      >
        Continue to Hotels →
      </n-button>
    </div>
  </div>
</template>

<style scoped>
.flight-selection {
  max-width: 800px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: var(--spacing-2xl);
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-md) 0;
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--text-light);
  margin: 0;
}

.flights-container {
  margin-bottom: var(--spacing-2xl);
}

.flight-card {
  cursor: pointer;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.flight-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.flight-card.selected {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(44, 123, 229, 0.1);
}

.flight-content {
  padding: var(--spacing-md);
}

.flight-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--spacing-lg);
}

.airline-info {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
}

.airline-logo {
  font-size: 2rem;
}

.airline-name {
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 var(--spacing-xs) 0;
}

.price-info {
  text-align: right;
}

.price {
  font-size: 2rem;
  font-weight: 700;
  color: var(--primary);
  display: block;
}

.price-unit {
  font-size: 0.9rem;
  color: var(--text-light);
}

.flight-details {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.time-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--spacing-md);
  background: var(--background);
  border-radius: var(--radius-md);
}

.departure, .arrival {
  text-align: center;
}

.time {
  font-size: 1.5rem;
  font-weight: 600;
  display: block;
}

.label {
  font-size: 0.9rem;
  color: var(--text-light);
}

.duration {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-xs);
  color: var(--text-light);
}

.stops {
  font-size: 0.8rem;
}

.features {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-sm);
}

.rating {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
  font-weight: 600;
}

.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }
  
  .flight-header {
    flex-direction: column;
    gap: var(--spacing-md);
  }
  
  .price-info {
    text-align: left;
  }
  
  .time-info {
    flex-direction: column;
    gap: var(--spacing-md);
  }
  
  .navigation {
    flex-direction: column;
    gap: var(--spacing-md);
  }
}
</style>