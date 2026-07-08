<template>
  <header :id="'header'" :class="{ scrolled: isScrolled }">
    <div class="container">
      <div class="nav-inner">
        <a href="#home" class="nav-logo" @click.prevent="scrollTo('home')">
          <span>Saliou</span><span>Diop</span>
        </a>

        <nav class="desktop-nav" role="navigation" aria-label="Navigation principale">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="nav-link"
            :class="{ active: activeSection === link.section, 'nav-cta': link.cta }"
            :id="'nav-' + link.section"
            @click.prevent="scrollTo(link.section)"
          >
            {{ link.label }}
          </a>
        </nav>

        <button
          id="mobile-menu-button"
          :aria-expanded="mobileOpen"
          aria-label="Ouvrir le menu"
          @click="toggleMobile"
        >
          <i :class="mobileOpen ? 'fas fa-times' : 'fas fa-bars'"></i>
        </button>
      </div>
    </div>

    <div id="mobile-menu" :class="{ open: mobileOpen }" role="navigation" aria-label="Navigation mobile">
      <a
        v-for="link in navLinks"
        :key="link.href"
        :href="link.href"
        class="nav-link"
        @click.prevent="mobileNav(link.section)"
      >
        {{ link.label }}
      </a>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const mobileOpen = ref(false)
const activeSection = ref('home')

const navLinks = [
  { href: '#home',     section: 'home',     label: 'Accueil' },
  { href: '#about',    section: 'about',    label: 'À propos' },
  { href: '#skills',   section: 'skills',   label: 'Compétences' },
  { href: '#projects', section: 'projects', label: 'Projets' },
  { href: '#contact',  section: 'contact',  label: 'Me contacter', cta: true },
]

function scrollTo(sectionId) {
  const el = document.getElementById(sectionId)
  if (el) {
    const offset = 72
    window.scrollTo({ top: el.offsetTop - offset, behavior: 'smooth' })
  }
  mobileOpen.value = false
}

function toggleMobile() {
  mobileOpen.value = !mobileOpen.value
}

function mobileNav(sectionId) {
  mobileOpen.value = false
  scrollTo(sectionId)
}

function onScroll() {
  isScrolled.value = window.scrollY > 20

  // Scroll spy
  const sections = ['home', 'about', 'skills', 'projects', 'contact']
  for (let i = sections.length - 1; i >= 0; i--) {
    const el = document.getElementById(sections[i])
    if (el && window.scrollY >= el.offsetTop - 200) {
      activeSection.value = sections[i]
      break
    }
  }
}

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>
