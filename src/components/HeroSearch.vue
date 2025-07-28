<script setup lang="ts">
import { ref, computed } from 'vue'
import { LocationOutline, CalendarOutline, PeopleOutline, CardOutline } from '@vicons/ionicons5'

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
    <div class="hero-content">
      <h1 class="hero-title">Where to next?</h1>
      <p class="hero-subtitle">
        Let's plan your perfect trip with AI-powered recommendations
      </p>

      <n-card class="search-card" size="large">
        <n-space vertical size="large">
          <!-- Destination -->
          <div class="input-group">
            <label class="input-label">
              <n-icon><LocationOutline /></n-icon>
              Where do you want to go?
            </label>
            <n-auto-complete
              v-model:value="destination"
              :options="destinationOptions.map(d => ({ label: d, value: d }))"
              placeholder="Enter your dream destination..."
              size="large"
              clearable
            />
          </div>

          <!-- Date Range -->
          <div class="input-group">
            <label class="input-label">
              <n-icon><CalendarOutline /></n-icon>
              When are you traveling?
            </label>
            <n-date-picker
              v-model:value="dateRange"
              type="daterange"
              size="large"
              placeholder="Select your travel dates"
              style="width: 100%"
            />
          </div>

          <!-- Trip Type -->
          <div class="input-group">
            <label class="input-label">
              <n-icon><PeopleOutline /></n-icon>
              What type of trip is this?
            </label>
            <n-select
              v-model:value="tripType"
              :options="tripTypes"
              placeholder="Choose your trip style"
              size="large"
            />
          </div>

          <!-- Budget (Optional) -->
          <div class="input-group">
            <label class="input-label">
              <n-icon><CardOutline /></n-icon>
              What's your budget? (Optional)
            </label>
            <n-select
              v-model:value="budget"
              :options="budgetOptions"
              placeholder="Select your budget range"
              size="large"
              clearable
            />
          </div>

          <!-- Action Button -->
          <div class="action-section">
            <n-button
              type="primary"
              size="large"
              :disabled="!canProceed"
              @click="handleNext"
              style="width: 100%; font-weight: 600;"
            >
              Start Planning My Trip ✈️
            </n-button>
            <p class="help-text">
              Don't worry, you can change these details later!
            </p>
          </div>
        </n-space>
      </n-card>
    </div>
  </div>
</template>

<style scoped>
.hero-search {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

.hero-content {
  padding: var(--spacing-lg) 0;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 var(--spacing-md) 0;
  background: linear-gradient(135deg, var(--primary), var(--accent-1));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: var(--text-light);
  margin: 0 0 var(--spacing-2xl) 0;
  line-height: 1.6;
}

.search-card {
  text-align: left;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  border: 0;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);
}

.input-label {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  font-weight: 600;
  color: var(--text);
  font-size: 1rem;
}

.action-section {
  margin-top: var(--spacing-lg);
}

.help-text {
  margin-top: var(--spacing-sm);
  font-size: 0.9rem;
  color: var(--text-light);
  text-align: center;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-subtitle {
    font-size: 1.1rem;
  }
}
</style>