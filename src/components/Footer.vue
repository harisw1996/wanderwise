<script setup lang="ts">
import { HeartOutline, MailOutline, LogoTwitter, LogoInstagram, LogoGithub } from '@vicons/ionicons5'
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <!-- Enhanced Logo & Description -->
        <div class="footer-section">
          <div class="footer-logo">
            <div class="logo-icon">
              <n-icon size="24" color="#2C7BE5">
                <HeartOutline />
              </n-icon>
            </div>
            <span class="logo-text">Wanderwise</span>
          </div>
          <p class="footer-description">
            Smart travel planning powered by AI. Make every journey unforgettable with personalized recommendations and intelligent itineraries.
          </p>
          <div class="social-links">
            <n-button quaternary circle class="social-btn">
              <template #icon>
                <n-icon><LogoTwitter /></n-icon>
              </template>
            </n-button>
            <n-button quaternary circle class="social-btn">
              <template #icon>
                <n-icon><LogoInstagram /></n-icon>
              </template>
            </n-button>
            <n-button quaternary circle class="social-btn">
              <template #icon>
                <n-icon><LogoGithub /></n-icon>
              </template>
            </n-button>
            <n-button quaternary circle class="social-btn">
              <template #icon>
                <n-icon><MailOutline /></n-icon>
              </template>
            </n-button>
          </div>
        </div>

        <!-- Enhanced Quick Links -->
        <div class="footer-section">
          <h4 class="footer-title">Quick Links</h4>
          <ul class="footer-links">
            <li><a href="#" class="footer-link">Home</a></li>
            <li><a href="#" class="footer-link">My Trips</a></li>
            <li><a href="#" class="footer-link">Explore Destinations</a></li>
            <li><a href="#" class="footer-link">Travel Guides</a></li>
            <li><a href="#" class="footer-link">Help Center</a></li>
          </ul>
        </div>

        <!-- Enhanced Support -->
        <div class="footer-section">
          <h4 class="footer-title">Support</h4>
          <ul class="footer-links">
            <li><a href="#" class="footer-link">Contact Us</a></li>
            <li><a href="#" class="footer-link">FAQ</a></li>
            <li><a href="#" class="footer-link">Travel Tips</a></li>
            <li><a href="#" class="footer-link">Booking Help</a></li>
            <li><a href="#" class="footer-link">Emergency Contacts</a></li>
          </ul>
        </div>

        <!-- Enhanced Legal -->
        <div class="footer-section">
          <h4 class="footer-title">Legal</h4>
          <ul class="footer-links">
            <li><a href="#" class="footer-link">Privacy Policy</a></li>
            <li><a href="#" class="footer-link">Terms of Service</a></li>
            <li><a href="#" class="footer-link">Cookie Policy</a></li>
            <li><a href="#" class="footer-link">Refund Policy</a></li>
            <li><a href="#" class="footer-link">Data Protection</a></li>
          </ul>
        </div>
      </div>

      <div class="footer-bottom">
        <div class="copyright">
          <span>© 2025 Wanderwise. Made with</span>
          <n-icon color="#DC3545" class="heart-icon">
            <HeartOutline />
          </n-icon>
          <span>for travelers worldwide.</span>
        </div>
        <div class="footer-badges">
          <span class="badge">AI-Powered</span>
          <span class="badge">Secure</span>
          <span class="badge">24/7 Support</span>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: linear-gradient(135deg, var(--text), #2c3e50);
  color: white;
  padding: var(--spacing-3xl) 0 var(--spacing-xl) 0;
  margin-top: auto;
  position: relative;
  overflow: hidden;
}

.footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="grain" width="100" height="100" patternUnits="userSpaceOnUse"><circle cx="50" cy="50" r="1" fill="rgba(255,255,255,0.02)"/></pattern></defs><rect width="100" height="100" fill="url(%23grain)"/></svg>');
  pointer-events: none;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: var(--spacing-3xl);
  margin-bottom: var(--spacing-2xl);
  position: relative;
  z-index: 1;
}

.footer-section {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
  margin-bottom: var(--spacing-md);
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

.logo-text {
  font-size: 1.8rem;
  font-weight: 800;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  letter-spacing: -0.5px;
}

.footer-description {
  color: #B0B0B0;
  line-height: 1.7;
  margin: 0;
  font-size: 1rem;
}

.social-links {
  display: flex;
  gap: var(--spacing-md);
  margin-top: var(--spacing-md);
}

.social-btn {
  transition: all 0.3s ease;
  background: rgba(255, 255, 255, 0.1) !important;
  border: 1px solid rgba(255, 255, 255, 0.2) !important;
}

.social-btn:hover {
  background: var(--gradient-primary) !important;
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(44, 123, 229, 0.3);
}

.footer-title {
  font-size: 1.2rem;
  font-weight: 700;
  margin: 0;
  color: white;
  position: relative;
  padding-bottom: var(--spacing-sm);
}

.footer-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 30px;
  height: 3px;
  background: var(--gradient-primary);
  border-radius: 2px;
}

.footer-links {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.footer-link {
  color: #B0B0B0;
  text-decoration: none;
  transition: all 0.3s ease;
  font-weight: 500;
  position: relative;
  padding-left: 0;
}

.footer-link::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  width: 0;
  height: 2px;
  background: var(--gradient-primary);
  transition: width 0.3s ease;
  transform: translateY(-50%);
}

.footer-link:hover {
  color: white;
  padding-left: var(--spacing-sm);
}

.footer-link:hover::before {
  width: 8px;
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: var(--spacing-xl);
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  z-index: 1;
}

.copyright {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  color: #B0B0B0;
  font-size: 0.95rem;
}

.heart-icon {
  animation: heartbeat 2s ease-in-out infinite;
}

@keyframes heartbeat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

.footer-badges {
  display: flex;
  gap: var(--spacing-md);
}

.badge {
  background: rgba(255, 255, 255, 0.1);
  color: white;
  padding: var(--spacing-xs) var(--spacing-md);
  border-radius: var(--radius-xl);
  font-size: 0.8rem;
  font-weight: 600;
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
}

.badge:hover {
  background: var(--gradient-primary);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-2xl);
  }
  
  .footer-section:first-child {
    text-align: center;
  }
  
  .social-links {
    justify-content: center;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: var(--spacing-lg);
    text-align: center;
  }
  
  .footer-badges {
    justify-content: center;
  }
}
</style>