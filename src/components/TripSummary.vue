<script setup lang="ts">
import { ref, computed } from 'vue'
import { 
  AirplaneOutline, 
  HomeOutline, 
  CalendarOutline, 
  LocationOutline,
  DownloadOutline,
  ShareOutline,
  PrintOutline
} from '@vicons/ionicons5'

const props = defineProps<{
  tripData: any
}>()

const emit = defineEmits<{
  prev: []
}>()

const formatDate = (timestamp: number) => {
  return new Date(timestamp).toLocaleDateString('en-US', {
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}

const tripDuration = computed(() => {
  if (!props.tripData.dates) return 0
  const [start, end] = props.tripData.dates
  return Math.ceil((end - start) / (1000 * 60 * 60 * 24))
})

const totalCost = computed(() => {
  let cost = 0
  if (props.tripData.selectedFlight) {
    cost += parseFloat(props.tripData.selectedFlight.price.replace('$', '').replace(',', ''))
  }
  if (props.tripData.selectedHotel) {
    const hotelPrice = parseFloat(props.tripData.selectedHotel.price.replace('$', ''))
    cost += hotelPrice * tripDuration.value
  }
  return cost
})

const exportTrip = (format: string) => {
  // Simulate export functionality
  console.log(`Exporting trip as ${format}`)
}

const shareTrip = () => {
  // Simulate sharing functionality
  console.log('Sharing trip')
}
</script>

<template>
  <div class="trip-summary">
    <div class="section-header">
      <h2 class="section-title">Your trip is ready! 🎉</h2>
      <p class="section-subtitle">
        Here's your complete travel plan for {{ tripData.destination }}
      </p>
    </div>

    <div class="summary-container">
      <!-- Trip Overview -->
      <n-card class="overview-card" size="large">
        <template #header>
          <div class="card-header">
            <n-icon size="24"><LocationOutline /></n-icon>
            Trip Overview
          </div>
        </template>

        <div class="overview-content">
          <div class="overview-item">
            <strong>Destination:</strong>
            <span>{{ tripData.destination }}</span>
          </div>
          <div class="overview-item">
            <strong>Duration:</strong>
            <span>{{ tripDuration }} days</span>
          </div>
          <div class="overview-item">
            <strong>Trip Type:</strong>
            <span>{{ tripData.tripType }}</span>
          </div>
          <div class="overview-item" v-if="tripData.dates">
            <strong>Dates:</strong>
            <span>{{ formatDate(tripData.dates[0]) }} - {{ formatDate(tripData.dates[1]) }}</span>
          </div>
          <div class="overview-item">
            <strong>Estimated Cost:</strong>
            <span class="cost">${{ totalCost.toLocaleString() }}</span>
          </div>
        </div>
      </n-card>

      <!-- Flight Details -->
      <n-card v-if="tripData.selectedFlight" class="detail-card">
        <template #header>
          <div class="card-header">
            <n-icon size="24"><AirplaneOutline /></n-icon>
            Your Flight
          </div>
        </template>

        <div class="flight-summary">
          <div class="flight-info">
            <h4>{{ tripData.selectedFlight.airline }}</h4>
            <p>{{ tripData.selectedFlight.departure }} - {{ tripData.selectedFlight.arrival }}</p>
            <p class="flight-meta">{{ tripData.selectedFlight.duration }} • {{ tripData.selectedFlight.stops }}</p>
          </div>
          <div class="flight-price">{{ tripData.selectedFlight.price }}</div>
        </div>
      </n-card>

      <!-- Hotel Details -->
      <n-card v-if="tripData.selectedHotel" class="detail-card">
        <template #header>
          <div class="card-header">
            <n-icon size="24"><HomeOutline /></n-icon>
            Your Accommodation
          </div>
        </template>

        <div class="hotel-summary">
          <div class="hotel-info">
            <h4>{{ tripData.selectedHotel.name }}</h4>
            <p>{{ tripData.selectedHotel.location }} • {{ tripData.selectedHotel.distance }}</p>
            <div class="hotel-features">
              <n-tag 
                v-for="feature in tripData.selectedHotel.features.slice(0, 3)" 
                :key="feature"
                size="small"
              >
                {{ feature }}
              </n-tag>
            </div>
          </div>
          <div class="hotel-price">
            <span class="rate">{{ tripData.selectedHotel.price }}/night</span>
            <span class="total">${{ (parseFloat(tripData.selectedHotel.price.replace('$', '')) * tripDuration).toLocaleString() }} total</span>
          </div>
        </div>
      </n-card>

      <!-- Itinerary Preview -->
      <n-card v-if="tripData.itinerary && tripData.itinerary.length > 0" class="detail-card">
        <template #header>
          <div class="card-header">
            <n-icon size="24"><CalendarOutline /></n-icon>
            Your Itinerary Highlights
          </div>
        </template>

        <div class="itinerary-preview">
          <div 
            v-for="day in tripData.itinerary.slice(0, 2)" 
            :key="day.day"
            class="day-preview"
          >
            <h4>Day {{ day.day }}: {{ day.title }}</h4>
            <ul class="activity-list">
              <li v-for="activity in day.activities.slice(0, 3)" :key="activity.title">
                {{ activity.time }} - {{ activity.title }}
              </li>
            </ul>
          </div>
          <p v-if="tripData.itinerary.length > 2" class="more-days">
            + {{ tripData.itinerary.length - 2 }} more days planned
          </p>
        </div>
      </n-card>

      <!-- Export & Share Options -->
      <n-card class="actions-card">
        <template #header>
          <div class="card-header">
            <n-icon size="24"><ShareOutline /></n-icon>
            Export & Share
          </div>
        </template>

        <n-space size="large">
          <n-button type="primary" size="large" @click="exportTrip('pdf')">
            <template #icon>
              <n-icon><DownloadOutline /></n-icon>
            </template>
            Download PDF
          </n-button>
          
          <n-button size="large" @click="exportTrip('email')">
            <template #icon>
              <n-icon><PrintOutline /></n-icon>
            </template>
            Email Itinerary
          </n-button>
          
          <n-button size="large" @click="shareTrip">
            <template #icon>
              <n-icon><ShareOutline /></n-icon>
            </template>
            Share Trip
          </n-button>
        </n-space>

        <n-divider />

        <div class="next-steps">
          <h4>Next Steps:</h4>
          <ul>
            <li>✅ Book your selected flight</li>
            <li>✅ Confirm hotel reservation</li>
            <li>📱 Download offline maps</li>
            <li>💳 Notify bank of travel dates</li>
            <li>📋 Check visa requirements</li>
          </ul>
        </div>
      </n-card>
    </div>

    <!-- Navigation -->
    <div class="navigation">
      <n-button @click="emit('prev')" size="large">
        ← Back to Itinerary
      </n-button>
      <n-button type="primary" size="large">
        Plan Another Trip
      </n-button>
    </div>
  </div>
</template>

<style scoped>
.trip-summary {
  max-width: 900px;
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

.summary-container {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-2xl);
}

.overview-card {
  background: linear-gradient(135deg, var(--primary), var(--accent-1));
  color: white;
}

.card-header {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  font-weight: 600;
  font-size: 1.2rem;
}

.overview-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-md);
}

.overview-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--spacing-sm) 0;
}

.overview-item strong {
  opacity: 0.9;
}

.cost {
  font-size: 1.2rem;
  font-weight: 700;
}

.detail-card {
  border-left: 4px solid var(--primary);
}

.flight-summary,
.hotel-summary {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: var(--spacing-lg);
}

.flight-info h4,
.hotel-info h4 {
  margin: 0 0 var(--spacing-sm) 0;
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text);
}

.flight-info p,
.hotel-info p {
  margin: 0 0 var(--spacing-xs) 0;
  color: var(--text-light);
}

.flight-meta {
  font-size: 0.9rem;
}

.flight-price {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary);
}

.hotel-features {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-xs);
  margin-top: var(--spacing-sm);
}

.hotel-price {
  text-align: right;
}

.rate {
  display: block;
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--primary);
}

.total {
  display: block;
  font-size: 0.9rem;
  color: var(--text-light);
  margin-top: var(--spacing-xs);
}

.itinerary-preview {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.day-preview h4 {
  margin: 0 0 var(--spacing-sm) 0;
  color: var(--text);
  font-weight: 600;
}

.activity-list {
  margin: 0;
  padding-left: var(--spacing-lg);
  list-style-type: none;
}

.activity-list li {
  padding: var(--spacing-xs) 0;
  color: var(--text-light);
  position: relative;
}

.activity-list li::before {
  content: "•";
  color: var(--primary);
  font-weight: bold;
  position: absolute;
  left: -var(--spacing-md);
}

.more-days {
  margin: var(--spacing-md) 0 0 0;
  color: var(--text-light);
  font-style: italic;
}

.actions-card {
  text-align: center;
}

.next-steps {
  text-align: left;
  margin-top: var(--spacing-lg);
}

.next-steps h4 {
  margin: 0 0 var(--spacing-md) 0;
  color: var(--text);
}

.next-steps ul {
  margin: 0;
  padding-left: var(--spacing-lg);
  list-style-type: none;
}

.next-steps li {
  padding: var(--spacing-xs) 0;
  color: var(--text-light);
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
  
  .overview-content {
    grid-template-columns: 1fr;
  }
  
  .flight-summary,
  .hotel-summary {
    flex-direction: column;
  }
  
  .hotel-price {
    text-align: left;
  }
  
  .navigation {
    flex-direction: column;
    gap: var(--spacing-md);
  }
}
</style>