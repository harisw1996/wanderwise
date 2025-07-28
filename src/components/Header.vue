<script setup lang="ts">
import { ref } from 'vue'
import { AirplaneOutline, MapOutline, CalendarOutline } from '@vicons/ionicons5'

const menuOptions = [
  { label: 'Home', key: 'home' },
  { label: 'My Trips', key: 'trips' },
  { label: 'Explore', key: 'explore' },
  { label: 'Help', key: 'help' }
]
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header-content">
        <!-- Logo -->
        <div class="logo">
          <n-icon size="28" color="#2C7BE5">
            <AirplaneOutline />
          </n-icon>
          <span class="logo-text">Wanderwise</span>
        </div>

        <!-- Desktop Navigation -->
        <nav class="desktop-nav">
          <n-menu
            mode="horizontal"
            :options="menuOptions"
            :root-indent="24"
          />
        </nav>

        <!-- User Actions -->
        <div class="user-actions">
          <n-button quaternary circle>
            <template #icon>
              <n-icon><CalendarOutline /></n-icon>
            </template>
          </n-button>
          <n-button type="primary" size="medium">
            Sign In
          </n-button>
        </div>

        <!-- Mobile Menu -->
        <div class="mobile-menu">
          <n-dropdown :options="menuOptions">
            <n-button quaternary circle>
              <template #icon>
                <n-icon><MapOutline /></n-icon>
              </template>
            </n-button>
          </n-dropdown>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  background: white;
  border-bottom: 1px solid var(--border);
  position: sticky;
  top: 0;
  z-index: 100;
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
}

.logo {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  font-weight: 700;
  font-size: 24px;
  color: var(--primary);
}

.logo-text {
  background: linear-gradient(135deg, var(--primary), var(--accent-1));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.desktop-nav {
  flex: 1;
  display: flex;
  justify-content: center;
  max-width: 400px;
  margin: 0 var(--spacing-lg);
}

.user-actions {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
}

.mobile-menu {
  display: none;
}

@media (max-width: 768px) {
  .desktop-nav {
    display: none;
  }
  
  .mobile-menu {
    display: block;
  }
  
  .user-actions {
    gap: var(--spacing-xs);
  }
}
</style>