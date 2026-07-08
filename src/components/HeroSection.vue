<template>
  <section id="home">
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>

    <div class="container">
      <div class="hero-content">
        <!-- Left -->
        <div>
          <div class="hero-badge">
            <span class="dot"></span>
            Disponible pour des opportunités
          </div>

          <h1 class="hero-name">
            Salut, je suis<br>
            <span class="gradient-text">Saliou Diop</span>
          </h1>

          <p class="hero-title">
            Développeur <strong>Full Stack</strong> &amp; UI/UX Designer
          </p>

          <p class="hero-desc">
            Étudiant en Informatique passionné par la création d'expériences web modernes et performantes.
            Spécialisé dans le développement web &amp; mobile, je transforme vos idées en solutions
            digitales élégantes.
          </p>

          <div class="hero-buttons">
            <a href="#contact" class="btn-primary" id="hero-contact-btn" @click.prevent="scrollTo('contact')">
              <i class="fas fa-paper-plane"></i>
              Me contacter
            </a>
            <a href="#projects" class="btn-secondary" id="hero-projects-btn" @click.prevent="scrollTo('projects')">
              <i class="fas fa-folder-open"></i>
              Mes projets
            </a>
          </div>

          <div class="hero-stats">
            <div class="stat-item" v-for="stat in stats" :key="stat.label">
              <div class="stat-number" :ref="el => statRefs[stat.label] = el">0+</div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
        </div>

        <!-- Right - Visual -->
        <div class="hero-visual">
          <div class="avatar-wrapper">
            <div class="avatar-ring"></div>
            <div class="avatar-circle">
              <img
              :src="avatarSrc"
              alt="Saliou Diop"
              @error="imgError = true"
              v-if="!imgError"
            />
              <div v-else class="avatar-icon-fallback"
                style="width:100%; height:100%; display:flex; align-items:center; justify-content:center; background: var(--accent-gradient-soft); border-radius:50%;">
                <span style="font-family:'Outfit',sans-serif; font-size:5rem; font-weight:900; background:var(--accent-gradient); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text;">SD</span>
              </div>
            </div>

            <!-- Floating tech badges -->
            <div class="floating-badge badge-laravel">
              <i class="fab fa-laravel" style="color:#ff2d20"></i> Laravel
            </div>
            <div class="floating-badge badge-django">
              <span style="font-weight:800; color:#0C4B33; font-size:0.9rem;">Dj</span> Django
            </div>
            <div class="floating-badge badge-express">
              <i class="fab fa-node-js" style="color:#3c873a"></i> Express.js
            </div>
            <div class="floating-badge badge-vue">
              <i class="fab fa-vuejs" style="color:#42b883"></i> Vue.js
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const imgError = ref(false)
const avatarSrc = '/portfolio.jpg'
const statRefs = ref({})

const stats = [
  { label: 'Projets réalisés', target: 9 },
  { label: 'Technologies',     target: 12 },
  { label: 'Années de formation', target: 3 },
]

function scrollTo(sectionId) {
  const el = document.getElementById(sectionId)
  if (el) window.scrollTo({ top: el.offsetTop - 72, behavior: 'smooth' })
}

function animateCounter(el, target) {
  let current = 0
  const step = Math.max(1, Math.floor(target / 40))
  const timer = setInterval(() => {
    current = Math.min(current + step, target)
    el.textContent = current + '+'
    if (current >= target) clearInterval(timer)
  }, 40)
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        stats.forEach(stat => {
          const el = statRefs.value[stat.label]
          if (el) animateCounter(el, stat.target)
        })
        observer.disconnect()
      }
    })
  }, { threshold: 0.5 })

  const section = document.getElementById('home')
  if (section) observer.observe(section)
})
</script>
