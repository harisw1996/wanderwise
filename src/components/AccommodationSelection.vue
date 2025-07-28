<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { HomeOutline, LocationOutline, StarOutline, WifiOutline } from '@vicons/ionicons5'

const props = defineProps<{
  tripData: any
}>()

const emit = defineEmits<{
  update: [data: any]
  next: []
  prev: []
}>()

const selectedHotel = ref(props.tripData.selectedHotel || null)
const loading = ref(true)

const hotels = ref([
  {
    id: 1,
    name: 'Grand Palace Hotel',
    image: 'https://images.pexels.com/photos/338504/pexels-photo-338504.jpeg?auto=compress&cs=tinysrgb&w=600',
    price: '$280',
    rating: 4.8,
    location: 'City Center',
    distance: '0.5 km from attractions',
    features: ['Free WiFi', 'Pool', 'Spa', 'Restaurant'],
    recommendation: 'Best Match',
    description: 'Luxury hotel in the heart of the city with world-class amenities.'
  },
  {
    id: 2,
    name: 'Budget Inn Express',
    image: 'https://images.pexels.com/photos/271618/pexels-photo-271618.jpeg?auto=compress&cs=tinysrgb&w=600',
    price: '$120',
    rating: 4.2,
    location: 'Downtown',
    distance: '2 km from attractions',
    features: ['Free WiFi', 'Breakfast', 'Clean rooms'],
    recommendation: 'Budget Pick',
    description: 'Comfortable and affordable with all essential amenities.'
  },
  {
    id: 3,
    name: 'Royal Suite Resort',
    image: 'https://images.pexels.com/photos/261102/pexels-photo-261102.jpeg?auto=compress&cs=tinysrgb&w=600',
    price: '$450',
    rating: 4.9,
    location: 'Beachfront',
    distance: '5 km from city center',
    features: ['Private beach', 'Butler service', 'Michelin restaurant', 'Helicopter pad'],
    recommendation: 'Luxury Pick',
    description: 'Ultimate luxury experience with unparalleled service and amenities.'
  }
])

onMounted(() => {
  setTimeout(() => {
    loading.value = false
  }, 1200)
})

const selectHotel = (hotel: any) => {
  selectedHotel.value = hotel
}

const handleNext = () => {
  if (selectedHotel.value) {
    emit('update', { selectedHotel: selectedHotel.value })
    emit('next')
  }
}
</script>

<template>
  <div class="accommodation-selection">
    <div class="section-header">
      <h2 class="section-title">Now let's find a place to rest and recharge</h2>
      <p class="section-subtitle">
        Perfect accommodations in {{ tripData.destination }}
      </p>
    </div>

    <n-spin :show="loading" size="large">
      <div class="hotels-container">
        <n-grid :cols="1" :x-gap="24" :y-gap="24">
          <n-grid-item v-for="hotel in hotels" :key="hotel.id">
            <n-card
              class="hotel-card"
              :class="{ 'selected': selectedHotel?.id === hotel.id }"
              hoverable
              @click="selectHotel(hotel)"
            >
              <div class="hotel-content">
                <!-- Hotel Image -->
                <div class="hotel-image">
                  <img :src="hotel.image" :alt="hotel.name" />
                  <n-tag 
                    v-if="hotel.recommendation"
                    class="recommendation-tag"
                    type="success"
                  >
                    {{ hotel.recommendation }}
                  </n-tag>
                </div>

                <!-- Hotel Info -->
                <div class="hotel-info">
                  <div class="hotel-header">
                    <h3 class="hotel-name">{{ hotel.name }}</h3>
                    <div class="price-section">
                      <span class="price">{{ hotel.price }}</span>
                      <span class="price-unit">per night</span>
                    </div>
                  </div>

                  <div class="hotel-meta">
                    <div class="rating">
                      <n-icon color="#FFC107"><StarOutline /></n-icon>
                      <span>{{ hotel.rating }}</span>
                    </div>
                    <div class="location">
                      <n-icon><LocationOutline /></n-icon>
                      <span>{{ hotel.location }} • {{ hotel.distance }}</span>
                    </div>
                  </div>

                  <p class="hotel-description">{{ hotel.description }}</p>

                  <div class="hotel-features">
                    <n-tag
                      v-for="feature in hotel.features"
                      :key="feature"
                      size="small"
                      round
                    >
                      {{ feature }}
                    </n-tag>
                  </div>
                </div>
              </div>
            </n-card>
          </n-grid-item>
        </n-grid>
      </div>
    </n-spin>

    <!-- Navigation -->
    <div class="navigation">
      <n-button @click="emit('prev')" size="large">
        ← Back to Flights
      </n-button>
      <n-button
        type="primary"
        :disabled="!selectedHotel"
        @click="handleNext"
        size="large"
      >
        Continue to Weather →
      </n-button>
    </div>
  </div>
</template>

<style scoped>
.accommodation-selection {
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

.hotels-container {
  margin-bottom: var(--spacing-2xl);
}

.hotel-card {
  cursor: pointer;
  transition: all 0.3s ease;
  border: 2px solid transparent;
  overflow: hidden;
}

.hotel-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.hotel-card.selected {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(44, 123, 229, 0.1);
}

.hotel-content {
  display: flex;
  gap: var(--spacing-lg);
}

.hotel-image {
  position: relative;
  flex-shrink: 0;
  width: 200px;
  height: 150px;
  border-radius: var(--radius-md);
  overflow: hidden;
}

.hotel-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.recommendation-tag {
  position: absolute;
  top: var(--spacing-sm);
  left: var(--spacing-sm);
}

.hotel-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.hotel-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.hotel-name {
  font-size: 1.5rem;
  font-weight: 600;
  margin: 0;
  color: var(--text);
}

.price-section {
  text-align: right;
}

.price {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary);
  display: block;
}

.price-unit {
  font-size: 0.9rem;
  color: var(--text-light);
}

.hotel-meta {
  display: flex;
  gap: var(--spacing-lg);
  align-items: center;
}

.rating, .location {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
  color: var(--text-light);
}

.hotel-description {
  margin: 0;
  color: var(--text-light);
  line-height: 1.6;
}

.hotel-features {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-sm);
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
  
  .hotel-content {
    flex-direction: column;
  }
  
  .hotel-image {
    width: 100%;
    height: 200px;
  }
  
  .hotel-header {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
  
  .price-section {
    text-align: left;
  }
  
  .navigation {
    flex-direction: column;
    gap: var(--spacing-md);
  }
}
</style>