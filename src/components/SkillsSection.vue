<template>
  <section id="skills">
    <div class="container">
      <h2 class="section-title reveal">Mes <span>compétences</span></h2>

      <div class="skills-grid reveal">
        <!-- Col 1: Frontend & Mobile -->
        <div class="skills-column">
          <h3>Frontend &amp; Mobile <span class="chip">UI/UX</span></h3>

          <div class="skill-item" v-for="skill in frontendSkills" :key="skill.name">
            <div class="skill-header">
              <span class="skill-name">
                <i :class="skill.icon" :style="{ color: skill.color }"></i>
                {{ skill.name }}
              </span>
              <span class="skill-pct">{{ skill.pct }}%</span>
            </div>
            <div class="skill-bar-bg">
              <div class="skill-bar-fill" :data-width="skill.pct"></div>
            </div>
          </div>
        </div>

        <!-- Col 2: Backend & Outils -->
        <div class="skills-column">
          <h3>Backend &amp; Outils <span class="chip">Core</span></h3>

          <div class="skill-item" v-for="skill in backendSkills" :key="skill.name">
            <div class="skill-header">
              <span class="skill-name">
                <i :class="skill.icon" :style="{ color: skill.color }"></i>
                {{ skill.name }}
              </span>
              <span class="skill-pct">{{ skill.pct }}%</span>
            </div>
            <div class="skill-bar-bg">
              <div class="skill-bar-fill" :data-width="skill.pct"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Tech Stack -->
      <div class="reveal">
        <p class="tech-stack-title">Technologies que j'utilise au quotidien</p>
        <div class="tech-stack-grid">
          <div class="tech-card" v-for="tech in techStack" :key="tech.name">
            <i :class="tech.icon" :style="{ color: tech.color }"></i>
            <span>{{ tech.name }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'

const frontendSkills = [
  { name: 'Vue.js',      icon: 'fab fa-vuejs',     color: '#42b883', pct: 75 },
  { name: 'JavaScript',  icon: 'fab fa-js',        color: '#d4a017', pct: 80 },
  { name: 'HTML / CSS',  icon: 'fab fa-html5',    color: '#e34f26', pct: 85 },
  { name: 'Flutter',     icon: 'fas fa-mobile-alt', color: '#54c5f8', pct: 65 },
  { name: 'WordPress',   icon: 'fab fa-wordpress', color: '#21759b', pct: 85 },
]

const backendSkills = [
  { name: 'Laravel',     icon: 'fab fa-laravel',   color: '#ff2d20', pct: 75 },
  { name: 'Django',      icon: 'fab fa-python',    color: '#0C4B33', pct: 65 },
  { name: 'Express.js',  icon: 'fab fa-node-js',   color: '#3c873a', pct: 65 },
  { name: 'SQL / MySQL', icon: 'fas fa-database',  color: '#00758f', pct: 75 },
  { name: 'Git & Figma', icon: 'fab fa-git-alt',   color: '#f05032', pct: 80 },
]

const techStack = [
  { name: 'Vue.js',     icon: 'fab fa-vuejs',       color: '#42b883' },
  { name: 'JavaScript', icon: 'fab fa-js',          color: '#d4a017' },
  { name: 'HTML5',      icon: 'fab fa-html5',      color: '#e34f26' },
  { name: 'CSS3',       icon: 'fab fa-css3-alt',   color: '#264de4' },
  { name: 'Flutter',    icon: 'fas fa-mobile-alt',  color: '#54c5f8' },
  { name: 'Laravel',    icon: 'fab fa-laravel',     color: '#ff2d20' },
  { name: 'Django',     icon: 'fab fa-python',      color: '#0C4B33' },
  { name: 'Express.js', icon: 'fab fa-node-js',     color: '#3c873a' },
  { name: 'WordPress',  icon: 'fab fa-wordpress',   color: '#21759b' },
  { name: 'MySQL',      icon: 'fas fa-database',    color: '#00758f' },
  { name: 'Figma',      icon: 'fab fa-figma',       color: '#f24e1e' },
  { name: 'Git',        icon: 'fab fa-git-alt',     color: '#f05032' },
]

onMounted(() => {
  // Reveal observer
  const revealObs = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') })
  }, { threshold: 0.1 })
  document.querySelectorAll('#skills .reveal').forEach(el => revealObs.observe(el))

  // Skill bar animation
  const skillObs = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const fill = entry.target
        const width = fill.getAttribute('data-width')
        setTimeout(() => { fill.style.width = width + '%' }, 200)
        skillObs.unobserve(fill)
      }
    })
  }, { threshold: 0.3 })

  document.querySelectorAll('#skills .skill-bar-fill').forEach(bar => skillObs.observe(bar))
})
</script>

<style scoped>
.skills-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px 60px;
  margin-bottom: 80px;
}

@media (max-width: 900px) {
  .skills-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}
</style>
