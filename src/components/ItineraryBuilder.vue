<script setup lang="ts">
import { ref, computed } from 'vue'
import { RestaurantOutline, CameraOutline, MapOutline, TimeOutline } from '@vicons/ionicons5'

const props = defineProps<{
  tripData: any
}>()

const emit = defineEmits<{
  update: [data: any]
  next: []
  prev: []
  skip: []
}>()

const preferences = ref({
  food: [] as string[],
  interests: [] as string[],
  pace: ''
})

const showItinerary = ref(false)
const generatedItinerary = ref<any[]>([])

const foodOptions = [
  { label: '🥗 Healthy Options', value: 'healthy' },
  { label: '🍖 Local Cuisine', value: 'local' },
  { label: '🍕 Street Food', value: 'street' },
  { label: '🌱 Vegetarian', value: 'vegetarian' },
  { label: '🥩 Halal', value: 'halal' },
  { label: '🍜 Fine Dining', value: 'fine' }
]

const interestOptions = [
  { label: '🏛️ History & Culture', value: 'history' },
  { label: '🌳 Nature & Parks', value: 'nature' },
  { label: '🛍️ Shopping', value: 'shopping' },
  { label: '🎨 Art & Museums', value: 'art' },
  { label: '👨‍👩‍👧‍👦 Family-friendly', value: 'family' },
  { label: '🌃 Nightlife', value: 'nightlife' },
  { label: '🏖️ Beach & Water', value: 'beach' },
  { label: '⛰️ Adventure Sports', value: 'adventure' }
]

const paceOptions = [
  { label: '😌 Relaxed (2-3 activities per day)', value: 'relaxed' },
  { label: '⚖️ Balanced (4-5 activities per day)', value: 'balanced' },
  { label: '🏃‍♂️ Packed (6+ activities per day)', value: 'packed' }
]

const canGenerate = computed(() => {
  return preferences.value.food.length > 0 && 
         preferences.value.interests.length > 0 && 
         preferences.value.pace
})

const generateItinerary = () => {
  // Simulate AI generation
  generatedItinerary.value = [
    {
      day: 1,
      title: 'Arrival & City Center',
      activities: [
        {
          time: '09:00',
          title: 'Check-in at Hotel',
          type: 'hotel',
          duration: '30 min',
          description: 'Settle in and freshen up'
        },
        {
          time: '10:30',
          title: 'Welcome Coffee',
          type: 'food',
          duration: '1 hour',
          description: 'Local café experience'
        },
        {
          time: '14:00',
          title: 'City Walking Tour',
          type: 'sightseeing',
          duration: '3 hours',
          description: 'Explore historic district'
        },
        {
          time: '19:00',
          title: 'Traditional Dinner',
          type: 'food',
          duration: '2 hours',
          description: 'Authentic local cuisine'
        }
      ]
    },
    {
      day: 2,
      title: 'Culture & Museums',
      activities: [
        {
          time: '09:00',
          title: 'National Museum',
          type: 'culture',
          duration: '2.5 hours',
          description: 'Art and history collection'
        },
        {
          time: '12:30',
          title: 'Museum Café Lunch',
          type: 'food',
          duration: '1 hour',
          description: 'Light lunch and relaxation'
        },
        {
          time: '15:00',
          title: 'Local Market Tour',
          type: 'shopping',
          duration: '2 hours',
          description: 'Shop for souvenirs and local goods'
        },
        {
          time: '18:00',
          title: 'Sunset Viewpoint',
          type: 'sightseeing',
          duration: '1 hour',
          description: 'Best views of the city'
        }
      ]
    }
  ]
  showItinerary.value = true
}

const getActivityIcon = (type: string) => {
  switch (type) {
    case 'food': return RestaurantOutline
    case 'sightseeing': return CameraOutline
    case 'culture': return MapOutline
    default: return TimeOutline
  }
}

const getActivityColor = (type: string) => {
  switch (type) {
    case 'food': return '#FFC107'
    case 'sightseeing': return '#2C7BE5'
    case 'culture': return '#00C9A7'
    case 'shopping': return '#DC3545'
    default: return '#6C757D'
  }
}

const handleNext = () => {
  emit('update', { 
    preferences: preferences.value,
    itinerary: generatedItinerary.value 
  })
  emit('next')
}
</script>

<template>
  <div class="itinerary-builder">
    <div class="section-header">
      <h2 class="section-title">Let's create your perfect itinerary</h2>
      <p class="section-subtitle">
        Tell us your preferences and we'll build a personalized day-by-day plan
      </p>
    </div>

    <div v-if="!showItinerary" class="preferences-section">
      <n-space vertical size="large">
        <!-- Food Preferences -->
        <n-card title="🍽️ Food Preferences" size="large">
          <n-checkbox-group v-model:value="preferences.food">
            <n-grid :cols="2" :x-gap="12" :y-gap="12">
              <n-grid-item v-for="option in foodOptions" :key="option.value">
                <n-checkbox :value="option.value" :label="option.label" />
              </n-grid-item>
            </n-grid>
          </n-checkbox-group>
        </n-card>

        <!-- Interest Preferences -->
        <n-card title="🎯 Your Interests" size="large">
          <n-checkbox-group v-model:value="preferences.interests">
            <n-grid :cols="2" :x-gap="12" :y-gap="12">
              <n-grid-item v-for="option in interestOptions" :key="option.value">
                <n-checkbox :value="option.value" :label="option.label" />
              </n-grid-item>
            </n-grid>
          </n-checkbox-group>
        </n-card>

        <!-- Travel Pace -->
        <n-card title="⏱️ Travel Pace" size="large">
          <n-radio-group v-model:value="preferences.pace">
            <n-space vertical>
              <n-radio 
                v-for="option in paceOptions" 
                :key="option.value"
                :value="option.value"
                :label="option.label"
              />
            </n-space>
          </n-radio-group>
        </n-card>

        <!-- Generate Button -->
        <div class="generate-section">
          <n-button
            type="primary"
            size="large"
            :disabled="!canGenerate"
            @click="generateItinerary"
            style="width: 100%;"
          >
            ✨ Generate My AI Itinerary
          </n-button>
        </div>
      </n-space>
    </div>

    <!-- Generated Itinerary -->
    <div v-else class="itinerary-section">
      <div class="itinerary-header">
        <h3>Your Personalized Itinerary</h3>
        <n-button @click="showItinerary = false">
          Edit Preferences
        </n-button>
      </div>

      <n-space vertical size="large">
        <n-card 
          v-for="day in generatedItinerary" 
          :key="day.day"
          class="day-card"
        >
          <template #header>
            <div class="day-header">
              <span class="day-number">Day {{ day.day }}</span>
              <span class="day-title">{{ day.title }}</span>
            </div>
          </template>

          <n-timeline>
            <n-timeline-item
              v-for="(activity, index) in day.activities"
              :key="index"
              :time="activity.time"
            >
              <template #icon>
                <n-icon :color="getActivityColor(activity.type)">
                  <component :is="getActivityIcon(activity.type)" />
                </n-icon>
              </template>
              
              <div class="activity-content">
                <h4 class="activity-title">{{ activity.title }}</h4>
                <p class="activity-description">{{ activity.description }}</p>
                <n-tag size="small" :color="{ color: getActivityColor(activity.type), textColor: 'white' }">
                  {{ activity.duration }}
                </n-tag>
              </div>
            </n-timeline-item>
          </n-timeline>
        </n-card>
      </n-space>
    </div>

    <!-- Navigation -->
    <div class="navigation">
      <n-button @click="emit('prev')" size="large">
        ← Back to Weather
      </n-button>
      <n-space>
        <n-button @click="emit('skip')" size="large">
          Skip Itinerary
        </n-button>
        <n-button
          type="primary"
          @click="handleNext"
          size="large"
          :disabled="!showItinerary"
        >
          Continue to Summary →
        </n-button>
      </n-space>
    </div>
  </div>
</template>

<style scoped>
.itinerary-builder {
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

.preferences-section {
  margin-bottom: var(--spacing-2xl);
}

.generate-section {
  text-align: center;
  margin-top: var(--spacing-xl);
}

.itinerary-section {
  margin-bottom: var(--spacing-2xl);
}

.itinerary-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-xl);
}

.itinerary-header h3 {
  font-size: 2rem;
  font-weight: 600;
  margin: 0;
  color: var(--text);
}

.day-card {
  border-left: 4px solid var(--primary);
}

.day-header {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
}

.day-number {
  background: var(--primary);
  color: white;
  padding: var(--spacing-xs) var(--spacing-md);
  border-radius: var(--radius-sm);
  font-weight: 600;
  font-size: 0.9rem;
}

.day-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text);
}

.activity-content {
  padding-left: var(--spacing-md);
}

.activity-title {
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0 0 var(--spacing-xs) 0;
  color: var(--text);
}

.activity-description {
  margin: 0 0 var(--spacing-sm) 0;
  color: var(--text-light);
  line-height: 1.5;
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
  
  .itinerary-header {
    flex-direction: column;
    gap: var(--spacing-md);
    text-align: center;
  }
  
  .day-header {
    flex-direction: column;
    text-align: center;
  }
  
  .navigation {
    flex-direction: column;
    gap: var(--spacing-md);
  }
}
</style>