<script setup lang="ts">
import { HeartOutline, MailOutline, LogoTwitter, LogoInstagram } from '@vicons/ionicons5'
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <!-- Logo & Description -->
        <div class="footer-section">
          <div class="footer-logo">
            <span class="logo-text">Wanderwise</span>
          </div>
          <p class="footer-description">
            Smart travel planning powered by AI. Make every journey unforgettable.
          </p>
          <div class="social-links">
            <n-button quaternary circle>
              <template #icon>
                <n-icon><LogoTwitter /></n-icon>
              </template>
            </n-button>
            <n-button quaternary circle>
              <template #icon>
                <n-icon><LogoInstagram /></n-icon>
              </template>
            </n-button>
            <n-button quaternary circle>
              <template #icon>
                <n-icon><MailOutline /></n-icon>
              </template>
            </n-button>
          </div>
        </div>

        <!-- Quick Links -->
        <div class="footer-section">
          <h4 class="footer-title">Quick Links</h4>
          <ul class="footer-links">
            <li><a href="#" class="footer-link">Home</a></li>
            <li><a href="#" class="footer-link">My Trips</a></li>
            <li><a href="#" class="footer-link">Explore</a></li>
            <li><a href="#" class="footer-link">Help Center</a></li>
          </ul>
        </div>

        <!-- Support -->
        <div class="footer-section">
          <h4 class="footer-title">Support</h4>
          <ul class="footer-links">
            <li><a href="#" class="footer-link">Contact Us</a></li>
            <li><a href="#" class="footer-link">FAQ</a></li>
            <li><a href="#" class="footer-link">Travel Tips</a></li>
            <li><a href="#" class="footer-link">Booking Help</a></li>
          </ul>
        </div>

        <!-- Legal -->
        <div class="footer-section">
          <h4 class="footer-title">Legal</h4>
          <ul class="footer-links">
            <li><a href="#" class="footer-link">Privacy Policy</a></li>
            <li><a href="#" class="footer-link">Terms of Service</a></li>
            <li><a href="#" class="footer-link">Cookie Policy</a></li>
            <li><a href="#" class="footer-link">Refund Policy</a></li>
          </ul>
        </div>
      </div>

      <div class="footer-bottom">
        <div class="copyright">
          <span>© 2025 Wanderwise. Made with</span>
          <n-icon color="#DC3545"><HeartOutline /></n-icon>
          <span>for travelers worldwide.</span>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--text);
  color: white;
  padding: var(--spacing-2xl) 0 var(--spacing-lg) 0;
  margin-top: auto;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: var(--spacing-2xl);
  margin-bottom: var(--spacing-xl);
}

.footer-section {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.footer-logo {
  margin-bottom: var(--spacing-sm);
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, var(--primary), var(--accent-1));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-description {
  color: #B0B0B0;
  line-height: 1.6;
  margin: 0;
}

.social-links {
  display: flex;
  gap: var(--spacing-sm);
  margin-top: var(--spacing-sm);
}

.footer-title {
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0;
  color: white;
}

.footer-links {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);
}

.footer-link {
  color: #B0B0B0;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: var(--primary);
}

.footer-bottom {
  border-top: 1px solid #404040;
  padding-top: var(--spacing-lg);
}

.copyright {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-xs);
  color: #B0B0B0;
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-xl);
  }
  
  .footer-section:first-child {
    text-align: center;
  }
  
  .social-links {
    justify-content: center;
  }
}
</style>