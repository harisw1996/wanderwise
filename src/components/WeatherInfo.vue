<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { SunnyOutline, CloudyOutline, RainyOutline, SnowOutline, ThermometerOutline } from '@vicons/ionicons5'

const props = defineProps<{
  tripData: any
}>()

const emit = defineEmits<{
  next: []
  prev: []
  skip: []
}>()

const loading = ref(true)
const weatherData = ref({
  location: '',
  current: {
    temp: 24,
    condition: 'Sunny',
    humidity: 65,
    windSpeed: 12
  },
  forecast: [
    { day: 'Today', temp: { high: 28, low: 18 }, condition: 'sunny', icon: 'sunny' },
    { day: 'Tomorrow', temp: { high: 26, low: 16 }, condition: 'partly-cloudy', icon: 'cloudy' },
    { day: 'Wed', temp: { high: 22, low: 14 }, condition: 'rainy', icon: 'rainy' },
    { day: 'Thu', temp: { high: 25, low: 17 }, condition: 'sunny', icon: 'sunny' },
    { day: 'Fri', temp: { high: 27, low: 19 }, condition: 'sunny', icon: 'sunny' },
    { day: 'Sat', temp: { high: 23, low: 15 }, condition: 'cloudy', icon: 'cloudy' },
    { day: 'Sun', temp: { high: 29, low: 20 }, condition: 'sunny', icon: 'sunny' }
  ]
})

const packingTips = ref([
  { item: '🧥 Light jacket', reason: 'Cool evenings expected' },
  { item: '☂️ Umbrella', reason: 'Rain possible on Wednesday' },
  { item: '🕶️ Sunglasses', reason: 'Sunny days ahead' },
  { item: '👕 Light clothing', reason: 'Warm temperatures' },
  { item: '🧴 Sunscreen', reason: 'Strong UV expected' }
])

onMounted(() => {
  weatherData.value.location = props.tripData.destination
  setTimeout(() => {
    loading.value = false
  }, 1000)
})

const getWeatherIcon = (condition: string) => {
  switch (condition) {
    case 'sunny': return SunnyOutline
    case 'cloudy': return CloudyOutline
    case 'rainy': return RainyOutline
    case 'snowy': return SnowOutline
    default: return SunnyOutline
  }
}

const getWeatherColor = (condition: string) => {
  switch (condition) {
    case 'sunny': return '#FFC107'
    case 'cloudy': return '#6C757D'
    case 'rainy': return '#2C7BE5'
    case 'snowy': return '#E3F2FD'
    default: return '#FFC107'
  }
}
</script>

<template>
  <div class="weather-info">
    <div class="section-header">
      <h2 class="section-title">Here's what the weather looks like</h2>
      <p class="section-subtitle">
        Weather forecast for your stay in {{ weatherData.location }}
      </p>
    </div>

    <n-spin :show="loading" size="large">
      <div class="weather-container">
        <!-- Current Weather -->
        <n-card class="current-weather-card" size="large">
          <div class="current-weather">
            <div class="current-info">
              <div class="temperature">
                <span class="temp-value">{{ weatherData.current.temp }}°</span>
                <span class="temp-unit">C</span>
              </div>
              <div class="condition">
                <n-icon size="48" :color="getWeatherColor('sunny')">
                  <SunnyOutline />
                </n-icon>
                <span class="condition-text">{{ weatherData.current.condition }}</span>
              </div>
            </div>
            <div class="weather-details">
              <div class="detail-item">
                <span class="label">Humidity</span>
                <span class="value">{{ weatherData.current.humidity }}%</span>
              </div>
              <div class="detail-item">
                <span class="label">Wind</span>
                <span class="value">{{ weatherData.current.windSpeed }} km/h</span>
              </div>
            </div>
          </div>
        </n-card>

        <!-- 7-Day Forecast -->
        <n-card class="forecast-card" title="7-Day Forecast">
          <div class="forecast-grid">
            <div 
              v-for="day in weatherData.forecast" 
              :key="day.day"
              class="forecast-day"
            >
              <div class="day-name">{{ day.day }}</div>
              <n-icon 
                size="24" 
                :color="getWeatherColor(day.icon)"
                class="weather-icon"
              >
                <component :is="getWeatherIcon(day.icon)" />
              </n-icon>
              <div class="temp-range">
                <span class="high">{{ day.temp.high }}°</span>
                <span class="low">{{ day.temp.low }}°</span>
              </div>
            </div>
          </div>
        </n-card>

        <!-- Packing Tips -->
        <n-card class="packing-card" title="Smart Packing Suggestions">
          <div class="packing-tips">
            <div 
              v-for="tip in packingTips" 
              :key="tip.item"
              class="tip-item"
            >
              <span class="tip-icon">{{ tip.item.split(' ')[0] }}</span>
              <div class="tip-content">
                <span class="tip-item-name">{{ tip.item.split(' ').slice(1).join(' ') }}</span>
                <span class="tip-reason">{{ tip.reason }}</span>
              </div>
            </div>
          </div>
        </n-card>
      </div>
    </n-spin>

    <!-- Navigation -->
    <div class="navigation">
      <n-button @click="emit('prev')" size="large">
        ← Back to Hotels
      </n-button>
      <n-space>
        <n-button @click="emit('skip')" size="large">
          Skip
        </n-button>
        <n-button type="primary" @click="emit('next')" size="large">
          Continue to Itinerary →
        </n-button>
      </n-space>
    </div>
  </div>
</template>

<style scoped>
.weather-info {
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

.weather-container {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-2xl);
}

.current-weather-card {
  background: linear-gradient(135deg, #2C7BE5, #00C9A7);
  color: white;
}

.current-weather {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.current-info {
  display: flex;
  align-items: center;
  gap: var(--spacing-xl);
}

.temperature {
  display: flex;
  align-items: baseline;
  gap: var(--spacing-xs);
}

.temp-value {
  font-size: 4rem;
  font-weight: 700;
}

.temp-unit {
  font-size: 2rem;
  opacity: 0.8;
}

.condition {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-sm);
}

.condition-text {
  font-size: 1.2rem;
  font-weight: 500;
}

.weather-details {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.detail-item {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.label {
  font-size: 0.9rem;
  opacity: 0.8;
}

.value {
  font-size: 1.2rem;
  font-weight: 600;
}

.forecast-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: var(--spacing-md);
}

.forecast-day {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-sm);
  padding: var(--spacing-md);
  border-radius: var(--radius-md);
  background: var(--background);
}

.day-name {
  font-weight: 600;
  font-size: 0.9rem;
  color: var(--text);
}

.weather-icon {
  margin: var(--spacing-xs) 0;
}

.temp-range {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
}

.high {
  font-weight: 600;
  color: var(--text);
}

.low {
  font-size: 0.9rem;
  color: var(--text-light);
}

.packing-tips {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--spacing-md);
}

.tip-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
  padding: var(--spacing-md);
  background: var(--background);
  border-radius: var(--radius-md);
}

.tip-icon {
  font-size: 1.5rem;
}

.tip-content {
  display: flex;
  flex-direction: column;
}

.tip-item-name {
  font-weight: 600;
  color: var(--text);
}

.tip-reason {
  font-size: 0.9rem;
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
  
  .current-weather {
    flex-direction: column;
    gap: var(--spacing-lg);
    text-align: center;
  }
  
  .forecast-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-sm);
  }
  
  .packing-tips {
    grid-template-columns: 1fr;
  }
  
  .navigation {
    flex-direction: column;
    gap: var(--spacing-md);
  }
}
</style>