<script setup lang="ts">
import { ref } from 'vue'
import { AirplaneOutline, MapOutline, CalendarOutline, PersonOutline } from '@vicons/ionicons5'

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
        <!-- Enhanced Logo -->
        <div class="logo">
          <div class="logo-icon">
            <n-icon size="32" color="#2C7BE5">
              <AirplaneOutline />
            </n-icon>
          </div>
          <span class="logo-text">Wanderwise</span>
        </div>

        <!-- Enhanced Desktop Navigation -->
        <nav class="desktop-nav">
          <n-menu
            mode="horizontal"
            :options="menuOptions"
            :root-indent="24"
            class="nav-menu"
          />
        </nav>

        <!-- Enhanced User Actions -->
        <div class="user-actions">
          <n-button quaternary circle class="action-btn">
            <template #icon>
              <n-icon><CalendarOutline /></n-icon>
            </template>
          </n-button>
          <n-button quaternary circle class="action-btn">
            <template #icon>
              <n-icon><PersonOutline /></n-icon>
            </template>
          </n-button>
          <n-button type="primary" size="medium" class="sign-in-btn">
            Sign In
          </n-button>
        </div>

        <!-- Enhanced Mobile Menu -->
        <div class="mobile-menu">
          <n-dropdown :options="menuOptions" trigger="click">
            <n-button quaternary circle class="mobile-menu-btn">
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
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border-light);
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.05);
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 72px;
}

.logo {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
  font-weight: 700;
  font-size: 28px;
  color: var(--primary);
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.05);
}

.logo-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  background: var(--gradient-primary);
  border-radius: var(--radius-lg);
  box-shadow: 0 4px 15px rgba(44, 123, 229, 0.3);
}

.logo-icon .n-icon {
  color: white !important;
}

.logo-text {
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 800;
  letter-spacing: -0.5px;
}

.desktop-nav {
  flex: 1;
  display: flex;
  justify-content: center;
  max-width: 500px;
  margin: 0 var(--spacing-xl);
}

.nav-menu {
  background: transparent !important;
}

.nav-menu :deep(.n-menu-item) {
  font-weight: 500;
  transition: all 0.3s ease;
}

.nav-menu :deep(.n-menu-item:hover) {
  background: rgba(44, 123, 229, 0.1) !important;
  border-radius: var(--radius-md);
}

.nav-menu :deep(.n-menu-item--selected) {
  background: var(--gradient-primary) !important;
  color: white !important;
  border-radius: var(--radius-md);
}

.user-actions {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
}

.action-btn {
  transition: all 0.3s ease;
}

.action-btn:hover {
  background: rgba(44, 123, 229, 0.1) !important;
  transform: translateY(-2px);
}

.sign-in-btn {
  background: var(--gradient-primary) !important;
  border: none !important;
  font-weight: 600;
  padding: 8px 20px;
  border-radius: var(--radius-md);
  transition: all 0.3s ease;
}

.sign-in-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(44, 123, 229, 0.3);
}

.mobile-menu {
  display: none;
}

.mobile-menu-btn {
  transition: all 0.3s ease;
}

.mobile-menu-btn:hover {
  background: rgba(44, 123, 229, 0.1) !important;
  transform: translateY(-2px);
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
  
  .logo {
    font-size: 24px;
  }
  
  .logo-icon {
    width: 40px;
    height: 40px;
  }
}
</style>