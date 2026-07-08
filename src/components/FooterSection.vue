<template>
  <footer>
    <div class="container">
      <div class="footer-inner">
        <div>
          <a href="#home" class="footer-logo" @click.prevent="scrollToTop">
            <span>Saliou</span><span style="color:var(--text-primary)">Diop</span>
          </a>
          <p style="color:var(--text-muted); font-size:0.85rem; margin-top:4px;">Développeur Full Stack · Dakar, Sénégal</p>
        </div>

        <p class="footer-copy">© 2025 Saliou Diop. Tous droits réservés.</p>

        <div class="footer-social">
          <a href="https://github.com/zalediop" class="social-icon" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
            <i class="fab fa-github"></i>
          </a>
          <a href="https://www.linkedin.com/in/saliou-diop-595799397/" class="social-icon" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
            <i class="fab fa-linkedin-in"></i>
          </a>
          <a href="https://www.instagram.com/_shaalihu_/" class="social-icon" target="_blank" rel="noopener noreferrer" aria-label="Instagram">
            <i class="fab fa-instagram"></i>
          </a>
          <a href="mailto:zalediop577@gmail.com" class="social-icon" aria-label="Email">
            <i class="fas fa-envelope"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>

  <!-- Back to Top -->
  <button id="back-to-top" :class="{ visible: showBackTop }" aria-label="Retour en haut" @click="scrollToTop">
    <i class="fas fa-arrow-up"></i>
  </button>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const showBackTop = ref(false)

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function onScroll() {
  showBackTop.value = window.scrollY > 400
}

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>
