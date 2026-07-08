<template>
  <div>
    <!-- Particles -->
    <div id="particles-js"></div>

    <NavBar />
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ProjectsSection />
    <ContactSection />
    <FooterSection />
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

onMounted(() => {
  // Initialize Particles.js
  if (typeof particlesJS !== 'undefined') {
    particlesJS('particles-js', {
      particles: {
        number: { value: 50, density: { enable: true, value_area: 900 } },
        color: { value: ['#6366f1', '#8b5cf6', '#06b6d4'] },
        shape: { type: 'circle' },
        opacity: { value: 0.4, random: true, anim: { enable: true, speed: 0.5, opacity_min: 0.1, sync: false } },
        size: { value: 2, random: true },
        line_linked: { enable: true, distance: 160, color: '#6366f1', opacity: 0.15, width: 1 },
        move: { enable: true, speed: 1, direction: 'none', random: true, out_mode: 'out' }
      },
      interactivity: {
        detect_on: 'canvas',
        events: {
          onhover: { enable: true, mode: 'grab' },
          onclick: { enable: true, mode: 'push' },
          resize: true
        },
        modes: {
          grab: { distance: 140, line_linked: { opacity: 0.6 } },
          push: { particles_nb: 2 }
        }
      },
      retina_detect: true
    })
  }

  // Global reveal observer
  const revealObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add('visible')
    })
  }, { threshold: 0.1 })
  document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el))
})
</script>
