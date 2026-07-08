<template>
  <section id="projects">
    <div class="container">
      <h2 class="section-title reveal">Mes <span>projets</span></h2>

      <div class="projects-filter reveal">
        <button
          v-for="f in filters"
          :key="f.value"
          class="filter-btn"
          :class="{ active: activeFilter === f.value }"
          :id="'filter-' + f.value"
          @click="setFilter(f.value)"
        >
          {{ f.label }}
        </button>
      </div>

      <TransitionGroup name="cards" tag="div" class="projects-grid">
        <div
          v-for="project in filteredProjects"
          :key="project.title"
          class="project-card"
        >
          <div class="project-image">
            <img :src="project.img" :alt="project.title" />
            <div class="project-image-overlay"></div>
          </div>
          <div class="project-body">
            <div class="project-header">
              <h3 class="project-title">{{ project.title }}</h3>
              <span
                v-for="badge in project.badges"
                :key="badge.label"
                class="project-badge"
                :class="'badge-' + badge.type"
              >
                {{ badge.label }}
              </span>
            </div>
            <p class="project-desc">{{ project.desc }}</p>
            <div class="project-tags">
              <span class="project-tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
            </div>
            <div class="project-actions" v-if="project.github || project.demo">
              <a
                v-if="project.github"
                :href="project.github"
                target="_blank"
                rel="noopener"
                class="btn-project btn-project-github"
              >
                <i class="fab fa-github"></i> GitHub
              </a>
              <a
                v-if="project.demo"
                :href="project.demo"
                target="_blank"
                rel="noopener"
                class="btn-project btn-project-demo"
              >
                <i class="fas fa-external-link-alt"></i> Demo
              </a>
            </div>
          </div>
        </div>
      </TransitionGroup>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const activeFilter = ref('all')

const filters = [
  { value: 'all',      label: 'Tous' },
  { value: 'vue',      label: 'Vue.js' },
  { value: 'frontend', label: 'Frontend' },
  { value: 'backend',  label: 'Backend' },
  { value: 'php',      label: 'PHP' },
  { value: 'mobile',   label: 'Mobile' },
  { value: 'design',   label: 'Design' },
  { value: 'cms',      label: 'CMS' },
]

const projects = [
  {
    category: 'vue',
    title: 'Gestion Hôtelière',
    badges: [{ label: 'Vue.js', type: 'vue' }],
    img: 'https://th.bing.com/th/id/R.22ce5dd214098b3f7a325d292e0ff164?rik=z%2bITy50UVm9NZA&riu=http%3a%2f%2fcheckinautomatique.com%2ffile%2fimg%2f562aca1d-bd74-4894-a133-beca4b6d87dc.webp&ehk=iDHYEZH5Bit0JOpxeTsvQA86nSVyNVy9HlsWAUkxizE%3d&risl=&pid=ImgRaw&r=0',
    desc: "Application web moderne développée avec Vue.js. Interface dynamique et réactive offrant une expérience utilisateur fluide et performante.",
    tags: ['Django', 'Vue.js', 'REST API'],
    github: 'https://github.com/zalediop/Keur_Absa',
    demo: null,
  },
  {
    category: 'vue',
    title: 'Gestion Navetanes',
    badges: [{ label: 'Express', type: 'vue' }, { label: 'Vue.js', type: 'vue' }],
    img: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1415&q=80',
    desc: "Plateforme web Vue.js déployée sur Vercel. Application interactive avec une architecture moderne et des composants réutilisables.",
    tags: ['HTML', 'CSS', 'Express.js'],
    github: 'https://github.com/zalediop/navmbour',
    demo: null,
  },
  {
    category: 'vue',
    title: 'SportLeague',
    badges: [{ label: 'Laravel', type: 'vue' }],
    img: 'https://images.unsplash.com/photo-1571019614242-c5c5dee9f50b?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80',
    desc: "Application de gestion de ligue sportive développée avec Laravel. Suivi des équipes, matchs et classements avec une interface intuitive.",
    tags: ['Vue.js', 'Laravel'],
    github: 'https://github.com/zalediop/SportLeague',
    demo: null,
  },
  {
    category: 'php',
    title: 'Pharma',
    badges: [{ label: 'PHP', type: 'php' }],
    img: 'https://images.unsplash.com/photo-1584308666744-24d5c474f2ae?ixlib=rb-4.0.3&auto=format&fit=crop&w=1430&q=80',
    desc: "Système de gestion pharmaceutique développé en PHP. Gestion des stocks, ordonnances et suivi des médicaments pour optimiser les opérations d'une pharmacie.",
    tags: ['PHP', 'MySQL', 'Gestion Stock'],
    github: 'https://github.com/zalediop/pharma',
    demo: null,
  },
  {
    category: 'backend',
    title: 'Gestion de Bibliothèque',
    badges: [{ label: 'Backend', type: 'backend' }],
    img: 'https://images.unsplash.com/photo-1481627834876-b7833e8f5570?ixlib=rb-4.0.3&auto=format&fit=crop&w=1528&q=80',
    desc: "Système CRUD complet de gestion de bibliothèque avec Laravel & Blade. Catalogage, gestion des emprunts, retours et membres avec interface d'administration.",
    tags: ['Laravel', 'Blade', 'MySQL', 'CRUD'],
    github: 'https://github.com/zalediop/gestion_bibliotheque',
    demo: null,
  },
  {
    category: 'frontend',
    title: 'Portfolio Personnel',
    badges: [{ label: 'Frontend', type: 'frontend' }],
    img: 'https://images.unsplash.com/photo-1467232004584-a241de8bcf5d?ixlib=rb-4.0.3&auto=format&fit=crop&w=1469&q=80',
    desc: "Ce portfolio moderne et animé développé en HTML, CSS et JavaScript vanilla. Design responsive avec animations, filtres projets et formulaire de contact.",
    tags: ['HTML5', 'CSS3', 'JavaScript', 'Responsive'],
    github: 'https://github.com/zalediop/updateportfolio',
    demo: 'https://updateportfolio-nu.vercel.app',
  },
  {
    category: 'mobile',
    title: 'NotesApp – Application Mobile',
    badges: [{ label: 'Mobile', type: 'mobile' }],
    img: 'https://images.unsplash.com/photo-1512941937669-90a1b58e7e9c?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80',
    desc: "Application mobile de gestion de notes développée avec Flutter et un backend Laravel. Fonctionnalités : création, modification et suppression de notes avec synchronisation API.",
    tags: ['Flutter', 'Laravel', 'API REST'],
    github: null,
    demo: null,
  },
  {
    category: 'design',
    title: 'UI/UX Design – App Assurance',
    badges: [{ label: 'Design', type: 'design' }],
    img: 'https://enozom.com/wp-content/uploads/2024/04/mobile-app-design-fundamentals-the-difference-between-UI-and-UX.webp',
    desc: "Maquette d'une application mobile permettant aux utilisateurs de souscrire à une assurance. Interface moderne, intuitive et centrée sur l'expérience utilisateur.",
    tags: ['Figma', 'UI Design', 'Prototypage'],
    github: null,
    demo: null,
  },
  {
    category: 'cms',
    title: 'Site E-commerce avec WordPress',
    badges: [{ label: 'CMS', type: 'cms' }],
    img: 'https://kinsta.com/fr/wp-content/uploads/sites/4/2023/08/woocommerce-elementor-1-1024x512.jpg',
    desc: "Boutique en ligne moderne avec système de panier et paiement sécurisé. Plugins utilisés : WooCommerce, Elementor, WPML, Yoast SEO pour une expérience utilisateur optimale.",
    tags: ['WordPress', 'WooCommerce', 'Elementor', 'Yoast SEO'],
    github: null,
    demo: null,
  },
]

const filteredProjects = computed(() => {
  if (activeFilter.value === 'all') return projects
  return projects.filter(p => p.category === activeFilter.value)
})

function setFilter(value) {
  activeFilter.value = value
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') })
  }, { threshold: 0.1 })
  document.querySelectorAll('#projects .reveal').forEach(el => observer.observe(el))
})
</script>

<style scoped>
/* TransitionGroup animations for project cards */
.cards-enter-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}
.cards-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
  position: absolute;
}
.cards-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
.cards-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

/* Keep grid layout correct during transitions */
.projects-grid {
  position: relative;
}
</style>
